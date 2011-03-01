#
#  Top Level Makefile for LAPACK
#  Version 3.1.1
#  February 2007
#

include make.inc

all: lapack_install lib lapack_testing blas_testing

lib: lapacklib tmglib
#lib: blaslib lapacklib tmglib

clean: cleanlib cleantesting cleanblas_testing 

lapack_install:
	( cd INSTALL; $(MAKE); ./testlsame; ./testslamch; \
	  ./testdlamch; ./testsecond; ./testdsecnd; ./testversion )

blaslib:
	( cd BLAS/SRC; $(MAKE) )

lapacklib:	lapack_install
	( cd SRC; $(MAKE) )

tmglib:
	( cd TESTING/MATGEN; $(MAKE) )

lapack_testing:	lib
	( cd TESTING ; $(MAKE) )

blas_testing:
	( cd BLAS/TESTING; $(MAKE) -f Makeblat1 )
	( cd BLAS; ./xblat1s > sblat1.out    ; \
	           ./xblat1d > dblat1.out    ; \
	           ./xblat1c > cblat1.out    ; \
	           ./xblat1z > zblat1.out    ) 
	( cd BLAS/TESTING; $(MAKE) -f Makeblat2 )
	( cd BLAS; ./xblat2s < sblat2.in     ; \
	           ./xblat2d < dblat2.in     ; \
	           ./xblat2c < cblat2.in     ; \
	           ./xblat2z < zblat2.in     )
	( cd BLAS/TESTING; $(MAKE) -f Makeblat3 )
	( cd BLAS; ./xblat3s < sblat3.in     ; \
	           ./xblat3d < dblat3.in     ; \
	           ./xblat3c < cblat3.in     ; \
	           ./xblat3z < zblat3.in     ) 

cleanlib:
	( cd INSTALL; $(MAKE) clean )
	( cd BLAS/SRC; $(MAKE) clean )
	( cd SRC; $(MAKE) clean )
	( cd TESTING/MATGEN; $(MAKE) clean )

cleanblas_testing:	
	( cd BLAS/TESTING; $(MAKE) -f Makeblat1 clean )
	( cd BLAS/TESTING; $(MAKE) -f Makeblat2 clean )
	( cd BLAS/TESTING; $(MAKE) -f Makeblat3 clean )
	( cd BLAS; rm -f xblat* )

cleantesting:
	( cd TESTING/LIN; $(MAKE) clean )
	( cd TESTING/EIG; $(MAKE) clean )
	( cd TESTING; rm -f xlin* xeig* )

cleanall: cleanlib cleanblas_testing cleantesting 
	rm -f *.a TESTING/*.out INSTALL/test*  BLAS/*.out

