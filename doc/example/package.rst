packaging
=========

Although one can use tox to develop and test applications one of its most popular
usage is to help library creators. Libraries need first to be packaged, so then
they can be installed inside a virtual environment for testing. To help with this
tox implements `PEP-517 <https://www.python.org/dev/peps/pep-0517/>`_ and
`PEP-518 <https://www.python.org/dev/peps/pep-0518/>`_. This means that by default
tox will build source distribution out of source trees. Before running test commands
``pip`` is used to install the source distribution inside the build environment.

To create a source distribution there are multiple tools out there and with ``PEP-517``
and ``PEP-518`` you can easily use your favorite one with tox. Historically tox
only supported ``setuptools``, and always used the tox host environment to build
a source distribution from the source tree. This is still the default behavior.
To opt out of this behaviour you need to set isolated builds to true.

setuptools
----------
Using the ``pyproject.toml`` file at the root folder (alongside ``setup.py``) one can specify
build requirements.

.. code-block:: toml

    [build-system]
    requires = [
        "setuptools >= 35.0.2",
        "setuptools_scm >= 2.0.0, <3"
    ]
    build-backend = "setuptools.build_meta"

.. code-block:: ini

   # tox.ini
   [tox]
   build_isolated = True

flit
----
`flit <https://flit.readthedocs.io/en/latest/>`_ requires ``Python 3``, however the generated source
distribution can be installed under ``python 2``. Furthermore it does not require a ``setup.py``
file as that information is also added to the ``pyproject.toml`` file.

.. code-block:: toml

    [build-system]
    requires = ["flit >= 1.1"]
    build-backend = "flit.buildapi"

    [tool.flit.metadata]
    module = "package_toml_flit"
    author = "Happy Harry"
    author-email = "happy@harry.com"
    home-page = "https://github.com/happy-harry/is"

.. code-block:: ini

   # tox.ini
   [tox]
   build_isolated = True
