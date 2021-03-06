.. _collect_licenses:

Collect licenses of dependencies
================================

With the ``imports`` feature it is possible to collect the License files from all packages in the dependency graph. Please note that the licenses are artifacts that must exist in the package binaries to be collected, as different package binaries might have different licenses. E.g., a package creator might provide a different license for static or shared linkage, they could provide different "License" files if they want to.

Also, we will assume the convention that the package authors will provide a "License" (case not important) file at the root of their packages.

In ``conanfile.txt`` we would use the following syntax:

.. code-block:: text

    [imports]
    ., license* -> ./licenses @ folder=True, ignore_case=True

And in ``conanfile.py`` we will use the ``imports()`` method:

.. code-block:: python

    def imports(self):
         self.copy("license*", dst="licenses", folder=True, ignore_case=True)

In both cases, after ``conan install``, it will store all the found License files inside the local **licenses** folder, wich will contain one subfolder per dependency with the license file inside.


