---
layout: post
title: Prex, an Elixir code generator.
---

Prex is a code generator for the API Blueprint documents. It generates Elixir module
to interact with your API. 

## What you up to?

Wow, It's my second elixir project in a about a week after [numero](https://github.com/alisinabh/numero). (Yayy!)

I don't know why i become creative when my exams start :|

## So what is it?

Prex is client code generator in elixir for whom is going to use a well documented API.

It can help developers save time and focus on their own issues instead of coding the API client.


Prex know ApiBlueprint language and can convert .apib files to elixir code.

Prex: [github.com/alisinabh/prex](https://github.com/alisinabh/prex)

ApiBlueprint: [apiblueprint.org](https://apiblueprint.org/)

## How you got idea?

Anyways, In last month i was dealing with REST Api services mostly from client perspective and i realized how much people don't care about documentation of their APIs. That's Crazy! There was even one company who hadn't any docs at all! They just sent me their real-time generated docs (seriously?) as we were talking on messenger and almost all of it were WRONG!

Especially most .NET developers in my country care much less about documenting. (I was a .net developer for 7 years. I know what i'm talking about)

## So what is the reason?

I think the first reason for that is education!

In colleges in IRAN there is absolutely no courses for documentation and if there is it's fairly outdated.

The second reason i think is the ecosystem. For example .NET ecosystem won't encourage a programmer to write good documents. There is no proper ways defined for documentations in that community. Even in C# learning videos no one talk about documentation in new features.

But take Elixir for example. It has a nice way of documenting your code. Its super friendly and in most Elixir tutorials they tech newbies about documentation and how important they are.

## How is Prex?

I've only started working on Prex for two days. But its fairly usable now since Prex itself is not going directly into your compiled code. It just generates code for you that you can customize and edit.

I'm planing on completely supporting ApiBlueprint data and adding tests based on examples in blueprint files. More importantly Prex is going to support SOAP and WSDL. :D

## Can you show us a sample?

Consider this example blueprint: [real-world-api.apib](https://apiblueprint.org/documentation/examples/real-world-api.html)

After running ``mix prex.gen.from_blueprint real-world-api.apib example`` Prex is going to generate following for you:

```elixir
lib/
└── example
   └── posts.ex
```

example/post.ex :

```elixir
# Created by Prex
defmodule Example.Posts do
  @moduledoc """
  This section groups App.net post resources.
  """

  @base_url "https://alpha-api.app.net"

  ###
  # API Calls
  ###

  # Post

  @doc """
  Returns a specific Post.

  ## Parameters
    - postid: The id of the Post.
  """
  def retrieve_a_post(postid \\ "") do
    req_url = Path.join @base_url, "/stream/0/posts/{post_id}"
    HTTPoison.request(:get, req_url, body: Poison.encode!(%{"post_id" => postid}), headers: ["Content-Type": "application/json"])
  end

  def retrieve_a_post!(postid \\ "") do
    {:ok, result} = retrieve_a_post(postid)
    result
  end

  @doc """
  Delete a Post. The current user must be the same user who created the Post. It
returns the deleted Post on success.

  ## Parameters
    - postid: The id of the Post.
  """
  def delete_a_post(postid \\ "") do
    req_url = Path.join @base_url, "/stream/0/posts/{post_id}"
    HTTPoison.request(:delete, req_url, body: Poison.encode!(%{"post_id" => postid}), headers: ["Content-Type": "application/json"])
  end

  def delete_a_post!(postid \\ "") do
    {:ok, result} = delete_a_post(postid)
    result
  end

  # Posts Collection

  @doc """
  Create a new Post object. Mentions and hashtags will be parsed out of the post
text, as will bare URLs...
  """
  def create_a_post do
    req_url = Path.join @base_url, "/stream/0/posts"
    HTTPoison.request(:post, req_url)
  end

  def create_a_post! do
    {:ok, result} = create_a_post()
    result
  end

  @doc """
  Retrieves all posts.
  """
  def retrieve_all_posts do
    req_url = Path.join @base_url, "/stream/0/posts"
    HTTPoison.request(:get, req_url)
  end

  def retrieve_all_posts! do
    {:ok, result} = retrieve_all_posts()
    result
  end

  # Stars

  @doc """
  Save a given Post to the current User’s stars. This is just a “save” action,
not a sharing action.

*Note: A repost cannot be starred. Please star the parent Post.*

  ## Parameters
    - postid: The id of the Post.
  """
  def star_a_post(postid \\ "") do
    req_url = Path.join @base_url, "/stream/0/posts/{post_id}/star"
    HTTPoison.request(:post, req_url, body: Poison.encode!(%{"post_id" => postid}), headers: ["Content-Type": "application/json"])
  end

  def star_a_post!(postid \\ "") do
    {:ok, result} = star_a_post(postid)
    result
  end

  @doc """
  Remove a Star from a Post.

  ## Parameters
    - postid: The id of the Post.
  """
  def unstar_a_post(postid \\ "") do
    req_url = Path.join @base_url, "/stream/0/posts/{post_id}/star"
    HTTPoison.request(:delete, req_url, body: Poison.encode!(%{"post_id" => postid}), headers: ["Content-Type": "application/json"])
  end

  def unstar_a_post!(postid \\ "") do
    {:ok, result} = unstar_a_post(postid)
    result
  end

end

```

Have fun integrating with APIs :)

