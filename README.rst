************************************
HSD — Human-friendly Structured Data
************************************

This Python package contains utilities to read and write files in
the Human-friendly Structured Data (HSD) format.

It is licensed under the *BSD 2-clause license*.


Installation
============

To install the python package in development mode use

.. code::

   pip install -e src


The HSD format
==============

The HSD-format is very similar to both JSON and XML, but tries to minimize the
effort for humans to read and write it. It ommits special characters as much as
possible but (in contrast to YAML for example) is not indentation dependent.

It was developed originally as the input format for a scientific simulation tool
(`DFTB+ <https://github.com/dftbplus/dftbplus>`_), but is absolutely general. A
typical input written in HSD looks like ::

  driver {
    conjugate_gradients {
      moved_atoms = 1 2 "7:19"
      max_steps = 100
    }
  }

  hamiltonian {
    dftb {
      scc = yes
      scc_tolerance = 1e-10
      mixer {
        broyden {}
      }
      filling {
        fermi {
          temperature [kelvin] = 1e-8
        }
      }
      k_points_and_weights {
        supercell_folding = {
          2   0   0
          0   2   0
          0   0   2
          0.5 0.5 0.5
        }
      }
    }
  }

Content in HSD format can be represented as JSON. Content in JSON format can
similarly be represented as HSD, provided it satisfies one restriction for
arrays: Either all elements of an array must be objects or none of them. (This
allows for a clear separation of structure and data and allows for the very
simple input format.)

Content in HSD format can be represented as XML (DOM-tree). Likewise content in
XML can be converted to HSD, provided it satisfies the restriction that every
child has either data (text) or further children, but never both of
them. (Again, this ensures the simplicity of the input format.)
