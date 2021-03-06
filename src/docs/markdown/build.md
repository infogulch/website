---
title: "Build from source"
---

# Build from source

Requirements:

- [Go](https://golang.org/dl) 1.14 or newer

Clone the repository:

<pre><code class="cmd bash">git clone "https://github.com/caddyserver/caddy.git"</code></pre>

If you don't have git, you can download the source code as a file archive [from GitHub](https://github.com/caddyserver/caddy). Each [release](https://github.com/caddyserver/caddy/releases) also has source snapshots.

Build:

<pre><code class="cmd"><span class="bash">cd caddy/cmd/caddy/</span>
<span class="bash">go build</span></code></pre>

<aside class="tip">
	Due to <a href="https://github.com/golang/go/issues/29228">a bug in Go</a>, these basic steps do not embed version information. If you want the version (<code>caddy version</code>), you need to compile Caddy as a dependency rather than as the main module. Instructions for this are in Caddy's <a href="https://github.com/caddyserver/caddy/blob/master/cmd/caddy/main.go">main.go</a> file. Or, you can use <b>xcaddy</b> which automates this.
</aside>

## xcaddy

The [`xcaddy` command](https://github.com/caddyserver/xcaddy) is the easiest way to build Caddy with version information and/or plugins.

Requirements:

- Go installed (see above)
- Make sure [xcaddy](https://github.com/caddyserver/xcaddy/releases) is in your PATH

You do **not** need to download the Caddy source code (it will do that for you).

Then building Caddy (with version information) is as easy as:

<pre><code class="cmd bash">xcaddy build</code></pre>

To build with plugins, use `--with`:

<pre><code class="cmd bash">xcaddy build \
    --with github.com/caddyserver/nginx-adapter
	--with github.com/caddyserver/ntlm-transport@v0.1.1</code></pre>

As you can see, you can customize the versions of plugins with `@` syntax. Versions can be a tag name or commit SHA.

Cross-platform compilation with `xcaddy` works the same as with the `go` command (see below).


## Cross-platform

Go programs are easy to compile for other platforms. Just set the `GOOS`, `GOARCH`, and/or `GOARM` environment variables that are different. ([See the go documentation for details.](https://golang.org/doc/install/source#environment))

For example, to compile Caddy for Windows when you're not on Windows:

<pre><code class="cmd bash">GOOS=windows go build</code></pre>

Or similarly for Linux ARMv6 when you're not on Linux or on ARMv6:

<pre><code class="cmd bash">GOOS=linux GOARCH=arm GOARM=6 go build</code></pre>

The same works for `xcaddy`. To cross-compile for macOS:

<pre><code class="cmd bash">GOOS=darwin xcaddy build</code></pre>
