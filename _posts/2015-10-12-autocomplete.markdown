---
layout: base
title: "Useful keyboard shortcut: autocomplete (⌥S)"
date: 2015-10-12
---

# Useful keyboard shortcut: autocomplete (⌥S)

<h2>Useful keyboard shortcut: autocomplete (⌥S)</h2>
<p>When filling out of text input, I often wish to accept the autocompletion provided. This requires hitting the down arrow to select the suggestion and then hitting enter to accept the completion. I don't like having to use arrow keys and I found myself doing this quite often, so I made a keyboard shortcut for accepting an autocompletion.</p>

<img src="/assets/html_demo.gif" alt="submit button demo">

<p>Using <a href="https://pqrs.org/osx/karabiner/">Karabiner</a> made this remap straightforward.
First, I remapped my right option key to a control key, since I use control key shortcuts frequently and my Macbook keyboard doesn&#39;t have a right control key.</p>

<img src="/assets/karabiner_options.png" alt="karabiner options">

<p>
I then added a remapping for control-s remap to my <code><a href="https://pqrs.org/osx/karabiner/xml.html.en">private.xml</a></code>:
</p>
<pre><code>&lt;item&gt;
  &lt;name&gt;Control s to down and submit&lt;/name&gt;
  &lt;identifier&gt;private.control_s_to_submit&lt;/identifier&gt;
  &lt;autogen&gt;__KeyToKey__
    KeyCode::S, ModifierFlag::CONTROL_R,
    KeyCode::CURSOR_DOWN,
    KeyCode::ENTER
  &lt;/autogen&gt;
&lt;/item&gt;
</code></pre>

<p>Now, whenever I want to choose the first autocomplete option, I simply hit ⌥S.</p>

<h2 id="using-with-fish-shell" href="#using-with-fish-shell">Using ⌥S with the <a href="http://fishshell.com/">fish shell</a></h2>

<p>I&#39;m a huge fan of <code>fish</code> autosuggestions, but having to use the right arrow key is similarly troublesome to using the down arrow. To allow the same keyboard shortcut to use <code>fish</code> completions as well, I modified the key remap to press the right arrow key first. This doesn't mess with conventional inputs since the cursor is already all the way to the right, and now ⌥S works in my shell as well.</p>

<div class="code-block">
<pre>&lt;item&gt;
  &lt;name&gt;Control s to right, down and submit&lt;/name&gt;
  &lt;identifier&gt;private.control_s_to_right_submit&lt;/identifier&gt;
  &lt;autogen&gt;__KeyToKey__
    KeyCode::S, ModifierFlag::CONTROL_R,
</pre>
<pre class="added">
    KeyCode::CURSOR_RIGHT,
</pre>
<pre><code>    KeyCode::CURSOR_DOWN,
    KeyCode::ENTER
  &lt;/autogen&gt;
&lt;/item&gt;
</code></pre>

<p>Here I type <code>py</code> and then ⌥S to run the suggested command.</p>

<img src="/assets/fish_demo.gif" alt="fish shell demo">

<p>You can find my full set of keyboard remaps at <a href="https://github.com/razzius/personal/blob/master/key_remaps/private.xml">https://github.com/razzius/personal/blob/master/key_remaps/private.xml</a>.</p>
</div>
