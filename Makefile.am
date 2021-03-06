AUTOMAKE_OPTIONS = subdir-objects

lib_LTLIBRARIES = libopus.la

SUBDIRS = . doc

INCLUDES = -I$(top_srcdir)/include -I$(top_srcdir)/celt -I$(top_srcdir)/silk -I$(top_srcdir)/silk/float -I$(top_srcdir)/silk/fixed

include celt_sources.mk
include silk_sources.mk
include opus_sources.mk

if FIXED_POINT
SILK_SOURCES += $(SILK_SOURCES_FIXED)
else
SILK_SOURCES += $(SILK_SOURCES_FLOAT)
endif

if OS_WINDOWS
NO_UNDEFINED = -no-undefined
endif

include celt_headers.txt
include silk_headers.txt
include opus_headers.txt

libopus_la_SOURCES = $(CELT_SOURCES) $(SILK_SOURCES) $(OPUS_SOURCES)
libopus_la_LDFLAGS = $(NO_UNDEFINED)

pkginclude_HEADERS = include/opus.h include/opus_multistream.h include/opus_types.h include/opus_defines.h

noinst_HEADERS = $(OPUS_HEAD) $(SILK_HEAD) $(CELT_HEAD)

noinst_PROGRAMS = opus_demo repacketizer_demo opus_compare tests/test_opus_api tests/test_opus_encode tests/test_opus_decode celt/tests/test_unit_cwrs32 celt/tests/test_unit_dft celt/tests/test_unit_entropy celt/tests/test_unit_laplace celt/tests/test_unit_mathops celt/tests/test_unit_mdct celt/tests/test_unit_rotation celt/tests/test_unit_types

TESTS = celt/tests/test_unit_types celt/tests/test_unit_mathops celt/tests/test_unit_entropy celt/tests/test_unit_laplace celt/tests/test_unit_dft celt/tests/test_unit_mdct celt/tests/test_unit_rotation celt/tests/test_unit_cwrs32 tests/test_opus_api tests/test_opus_decode tests/test_opus_encode

opus_demo_SOURCES = src/opus_demo.c

opus_demo_LDADD = libopus.la -lm

repacketizer_demo_SOURCES = src/repacketizer_demo.c

repacketizer_demo_LDADD = libopus.la -lm

opus_compare_SOURCES = src/opus_compare.c
opus_compare_LDADD = -lm

tests_test_opus_api_SOURCES = tests/test_opus_api.c tests/test_opus_common.h
tests_test_opus_api_LDADD = libopus.la -lm

tests_test_opus_encode_SOURCES = tests/test_opus_encode.c tests/test_opus_common.h
tests_test_opus_encode_LDADD = libopus.la -lm

tests_test_opus_decode_SOURCES = tests/test_opus_decode.c tests/test_opus_common.h
tests_test_opus_decode_LDADD = libopus.la -lm

celt_tests_test_unit_cwrs32_SOURCES = celt/tests/test_unit_cwrs32.c
celt_tests_test_unit_cwrs32_LDADD = -lm

celt_tests_test_unit_dft_SOURCES = celt/tests/test_unit_dft.c
celt_tests_test_unit_dft_LDADD = -lm

celt_tests_test_unit_entropy_SOURCES = celt/tests/test_unit_entropy.c
celt_tests_test_unit_entropy_LDADD = -lm

celt_tests_test_unit_laplace_SOURCES = celt/tests/test_unit_laplace.c
celt_tests_test_unit_laplace_LDADD = -lm

celt_tests_test_unit_mathops_SOURCES = celt/tests/test_unit_mathops.c
celt_tests_test_unit_mathops_LDADD = -lm

celt_tests_test_unit_mdct_SOURCES = celt/tests/test_unit_mdct.c
celt_tests_test_unit_mdct_LDADD = -lm

celt_tests_test_unit_rotation_SOURCES = celt/tests/test_unit_rotation.c
celt_tests_test_unit_rotation_LDADD = -lm

celt_tests_test_unit_types_SOURCES = celt/tests/test_unit_types.c
celt_tests_test_unit_types_LDADD = -lm

if CUSTOM_MODES
pkginclude_HEADERS += include/opus_custom.h
noinst_PROGRAMS += opus_custom_demo
opus_custom_demo_SOURCES = celt/opus_custom_demo.c
opus_custom_demo_LDADD = libopus.la -lm
endif

EXTRA_DIST = opus.pc.in opus-uninstalled.pc.in

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = opus.pc
