=============
Release notes
=============

-----------
modred 1.1a
-----------
Done by Pierre Augier (pa371 @ damtp.cam.ac.uk). The 'a' means
alpha. It is a testing version.

**New features and improvements**

* None

**Bug fixes**

* A bug in the function ``modred.util.impulse``.

**Interface changes**

* None

**Internal changes**

* The packaging has been improved.

* Ported to python >= 3.3 using `python-future
  <http://python-future.org/>`_.

------------
modred 1.0.2
------------
We increased the speed of the BPOD implementations. 

**New features and improvements**

* None

**Bug fixes**

* None

**Interface changes**

* None

**Internal changes**

* BPOD classes now compute fewer inner products. The number of inner products 
  is now the sum of the number of direct vectors and the number of adjoint 
  vectors, whereas previously it was the product. This is achieved by taking
  advantage of a property of the adjoint. 


------------
modred 1.0.1
------------
Small changes mostly related to examples.

**New features and improvements**

* None

**Bug fixes**

* Changed a tutorial example. 

**Interface changes**

* None

**Internal changes**

* None



------------
modred 1.0.0
------------
Many interface changes including new classes and functions for different
sized data.

**New features and improvements**

* New functions and classes for data that fits entirely on one node's memory. 
  These are
  :py:func:`pod.compute_POD_matrices_snaps_method`, 
  :py:func:`pod.compute_POD_matrices_direct_method`,
  :py:func:`bpod.compute_BPOD_matrices`, 
  :py:func:`dmd.compute_DMD_matrices_snaps_method`, 
  :py:func:`dmd.compute_DMD_matrices_direct_method`,
  :py:class:`ltigalerkinproj.LTIGalerkinProjectionMatrices`, and
  :py:class:`vectorspace.VectorSpaceMatrices`.
  These replace the ``in_memory`` member functions and improve 
  computational efficiency for small data.

* Added balanced truncation :py:meth:`util.balanced_truncation`.


**Bug fixes**

* None


**Interface changes**

* The old classes ``POD``, ``BPOD``, ``DMD``,  
  are now only for large data and have their names appended with "``Handles``".

* Old classes ``LTIGalerkinProjection``, and ``VectorSpace``
  have been split into two, and names appended with "``Matrices``" and 
  "``Handles``".
  
* All ``in_memory`` member functions have been removed, replaced by 
  the functions and classes above.

* Removed the ``index_from`` optional argument in ``compute_modes`` functions. 
  Mode numbers are now always indexed from zero and are renamed mode indices.

* The ``VectorSpace`` member function ``compute_modes`` has
  been removed and its functionality moved to ``lin_combine``.

* ``LTIGalerkinProjection`` member function ``compute_model`` uses the
  result of an operator on a vector, 
  rather than the operator itself. See 
  :py:meth:`ltigalerkinproj.LTIGalerkinProjectionHandles.compute_model`.
  The operator classes have been removed.


**Internal changes**

* OKID now uses least squares instead of a pseudo-inverse for improved numerical
  stability. 

* Added :py:class:`util.InnerProductBlock` for testing.



------------
modred 0.3.2
------------
The main change is a bug fix in :py:meth:`util.lsim`.

**New features and improvements**

None

**Bug fixes**

* Function :py:meth:`util.lsim`, which is only provided for the user's convenience, 
  is simplified and corrected.

**Interface changes**

* :py:meth:`util.lsim`.


**Internal changes**

None


------------
modred 0.3.1
------------
The main change is a bug fix in the ``numpy.eigh`` wrapper, :py:meth:`util.eigh`.

**New features and improvements**

None

**Bug fixes**

* The POD and DMD classes now use :py:meth:`util.eigh` with the 
  ``is_positive_definite`` flag 
  set to ``True``.  This eliminates the possibility of small negative eigenvalues
  that sometimes appear due to numerical precision which led to errors.

**Interface changes**

None


**Internal changes**

* Function :py:meth:`util.eigh` now has a flag for positive definite matrices.  
  When
  ``True``, the function will automatically adjust the tolerance such that only
  positive eigenvalues are returned.


------------
modred 0.3.0
------------

**New features and improvements**

* New class :py:class:`ltigalerkinproj.LTIGalerkinProjection`
  for LTI Galerkin projections. Replaces and generalizes old class ``BPODLTIROM``.

* Improved print messages to print every 10 seconds and be more informative.

**Bug fixes**

* Corrected small error in symmetric inner product matrix calculation (used
  by POD and DMD) where some very small matrix entries were double the true 
  value. 

* Fixed race condition in :py:meth:`vectorspace.VectorSpace.lin_combine` by adding
  a barrier.
  
**Interface changes**

* Removed class ``BPODLTIROM``.

* Changed order of indices in Markov parameters returned by :py:meth:`okid.OKID`.

* Changed all uses of ``hankel`` to ``Hankel`` to be consistent with naming 
  convention.
  
**Internal changes**

* Added :py:meth:`parallel.Parallel.call_and_bcast` method to ``Parallel`` class.

* Changed interface of :py:meth:`helper.add_to_path`.

* :py:class:`dmd.DMD` no longer uses an instance of :py:class:`pod.POD`. 

* The equals operator of vector handles now better deals with vectors which
  are numpy array objects.


------------
modred 0.2.1
------------

No noteworthy changes from v0.2.0, figuring out pypi website.

------------
modred 0.2.0
------------

First publicly available version.
