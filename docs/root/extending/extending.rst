.. _extending:

Extending Envoy for custom use cases
====================================

Envoy doesn't cover all use cases out of the box and was built with extensibility in mind.
To extend Envoy, you can create your own:

* :ref:`HTTP filters <arch_overview_http_filters>` for encoding and decoding HTTP traffic
* :ref:`Network filters <arch_overview_network_filters>` for non-HTTP traffic

.. note::

  If you're interested in example extensions, see the `envoy-filter-example
  <https://github.com/envoyproxy/envoy-filter-example>`_ project and the `extensions
  <https://github.com/envoyproxy/envoy/tree/master/source/extensions>`_ subdirectory in the
  main Envoy repository. We'll cover building extensions in a step-by-step way in this
  guide, but those projects are good reference points for 

How extension works
^^^^^^^^^^^^^^^^^^^

When you extend Envoy, you essentially build an Envoy binary but with your new
filters added. Creating extensions thus requires you to build all of standard Envoy
*plus* your custom logic.

Getting started
^^^^^^^^^^^^^^^

The easiest way to get started building an extension is to:

1. Add the main Envoy repository as a `Git submodule
    <https://git-scm.com/book/en/v2/Git-Tools-Submodules>`_ in your project. This gives you
    a mechanism for keeping the Envoy code up to date.
2. Build your extended Envoy binary using `Bazel <https://bazel.build>`_, the multi-language
    build tool used for the Envoy project.

Here's an example:

.. code-block:: bash

  mkdir custom-envoy-filter && cd custom-envoy-filter
  git submodule add https://github.com/envoyproxy/envoy
