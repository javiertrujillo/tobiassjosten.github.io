---
layout: post
title: Symfony plugin for Flattr
category: symfony
tags: [symfony, flattr]
summary: I just finished writing some documentation for my first Symfony plugin – sfFlattrPlugin! I encourage you to try it out and let me know what you think. Everything is up at GitHub, which means that you can easily share whatever improvements you conjure up.
---
I just finished writing [some documentation](http://github.com/tobiassjosten/sfFlattrPlugin#readme) for my first [Symfony](http://www.symfony-project.org/) plugin – [sfFlattrPlugin](http://github.com/tobiassjosten/sfFlattrPlugin)! I encourage you to try it out and let me know what you think. Everything is up at GitHub, which means that you can easily share whatever improvements you conjure up.

This Symfony plugin enables easy to use integration with the [Flattr service](http://flattr.com/). Specifically, it provides a helper function to create Flattr buttons.

## Installation

I recommend installing the plugin as a Git submodule:

    $ git submodule add plugins/sfFlattrPlugin http://github.com/tobiassjosten/sfFlattrPlugin.git

Then you add it to your list of enabled plugins:

    // config/ProjectConfiguration.class.php
    class ProjectConfiguration extends sfProjectConfiguration
    {
      public function setup()
      {
        $this->enablePlugins('sfFlattrPlugin');
      }
    }

And finally you add it you you filter chain:

    # apps/frontend/config/filters.yml
    rendering: ~
    security:  ~
      sf_flattr_plugin:
        class: sfFlattrFilter
    cache:     ~
    execution: ~

## Configuration

There are three ways to configure your Flattr buttons. You can either do it in `app.yml`, when you create buttons or a mix of the two.

These are the settings you can use in your `app.yml`:

    all:
      sf_flattr_plugin:
        # Required
        uid:         User ID on Flattr.
        title:       The title of your item.
        description: A description of your item.
        category:    text, images, video, audio, software or rest
        # Optional
        language:    Language of the item, using syntax 'en_GB'.
        tags:        Comma seperated,list of,tags
        button:      normal (default) or compact
        hidden:      1 to hide, 0 (default) to show on Flattr.com listing
        html5:       false

## Usage

Creating a Flattr buttons involves first including the helper. Either in your `settings.yml`:

    # apps/frontend/config/settings.yml
    all:
      .settings:
        standard_helpers:
          - Flattr

... or directly in your view:

    <?php use_helper('Flattr') ?>

And then you may use the helper. Here is an example with most of the configuration options either instead of or to override settings in `app.yml`:

    flattr_button(url_for('my_route', $item, true), array(
      'uid' => 'tobiassjosten',
      'title' => 'Example title',
      'description' => 'A very descriptive text',
      'category' => 'text',
      'button' => 'compact',
      'html5' => false,
      'data' => array('button' => 'compact'),
    ));

Simple as that!
