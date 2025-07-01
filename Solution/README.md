# Puzzle #82: State Laws

Carl and Jeff want to know why strange things are happening when using an injected StateBag service.

YouTube Video: https://youtu.be/

Blazor Puzzle Home Page: https://blazorpuzzle.com

## The Challenge

This is a .NET 9 Blazor Web App with global server interactivity

We have moved the currentCount variable out of the Counter.razor page and into a StateBag service that we have injected. We now use the StateBag.Counter property.

This is so we can keep track of the Count when we navigate away from and back to the Counter page.

We have added StateBag as a service so it can be injected, and it works. Kind of.

If we load another session, it seems to be sharing the state data with the other sessions.

How can we fix this?

## The Solution

The solution is simple, yet it may be unintuitive if you have little experience working with server-side Blazor.

Change line 10 in *Program.cs* from this:

```c#
builder.Services.AddSingleton<StateBag>();
```

to this:

```c#
builder.Services.AddScoped<StateBag>();
```

In a Blazor Server app, Singleton services provide one instance of a class that is shared with all the users.

Scoped services provide one instance PER user.

Boom!
