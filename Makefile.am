warning_flags = -Wall -Wextra -Wshadow -Wno-unused-parameter
common_cflags = -O3 -ffast-math -fvisibility=hidden $(warning_flags) $(MFLAGS)
AM_CXXFLAGS = -std=c++14 $(common_cflags)

AM_CPPFLAGS = $(VapourSynth_CFLAGS)

lib_LTLIBRARIES = libyadifmod.la

libyadifmod_la_SOURCES = Yadifmod/Yadifmod.cpp \
                         Yadifmod/vectorclass/instrset.h \
                         Yadifmod/vectorclass/instrset_detect.cpp

if VS_TARGET_CPU_X86
libyadifmod_la_SOURCES += Yadifmod/Yadifmod_SSE2.cpp \
                          Yadifmod/vectorclass/vectorclass.h \
                          Yadifmod/vectorclass/vectorf128.h \
                          Yadifmod/vectorclass/vectorf256.h \
                          Yadifmod/vectorclass/vectorf256e.h \
                          Yadifmod/vectorclass/vectori128.h \
                          Yadifmod/vectorclass/vectori256.h \
                          Yadifmod/vectorclass/vectori256e.h

noinst_LTLIBRARIES = libavx.la libavx2.la

libavx_la_SOURCES = Yadifmod/Yadifmod_AVX.cpp
libavx_la_CXXFLAGS = $(AM_CXXFLAGS) -mavx

libavx2_la_SOURCES = Yadifmod/Yadifmod_AVX2.cpp
libavx2_la_CXXFLAGS = $(AM_CXXFLAGS) -mavx2 -mfma

libyadifmod_la_LIBADD = libavx.la libavx2.la
endif

libyadifmod_la_LDFLAGS = -no-undefined -avoid-version $(PLUGINLDFLAGS)
