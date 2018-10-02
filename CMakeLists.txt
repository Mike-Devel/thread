# Copyright 2018 Mike Dev
# Distributed under the Boost Software License, Version 1.0.
# See accompanying file LICENSE_1_0.txt or copy at http://www.boost.org/LICENSE_1_0.txt

cmake_minimum_required(VERSION 3.5)
project(BoostThread LANGUAGES CXX)

file(GLOB BOOST_THREAD_SRC_PTHREAD src/pthread/*.cpp)
file(GLOB BOOST_THREAD_SRC_WIN32 src/win32/*.cpp)

if(WIN32)
    set(BOOST_THREAD_SRC_PLATFORM ${BOOST_THREAD_SRC_WIN32})
else()
    set(BOOST_THREAD_SRC_PLATFORM ${BOOST_THREAD_SRC_PTHREAD})
endif()

add_library(boost_thread
    src/future.cpp
    src/tss_null.cpp
    ${BOOST_THREAD_SRC_PLATFORM}
)
add_library(Boost::thread ALIAS boost_thread)

target_include_directories(boost_thread PUBLIC include)

target_link_libraries(boost_thread
    PUBLIC
        Boost::assert
        Boost::atomic
        Boost::bind
        Boost::chrono
        Boost::concept_check
        Boost::config
        Boost::container
        Boost::container_hash
        Boost::core
        Boost::date_time
        Boost::exception
        Boost::function
        Boost::intrusive
        Boost::io
        Boost::iterator
        Boost::move
        Boost::mpl
        Boost::optional
        Boost::predef
        Boost::preprocessor
        Boost::smart_ptr
        Boost::static_assert
        Boost::system
        Boost::throw_exception
        Boost::tuple
        Boost::type_traits
        Boost::utility
        Boost::winapi
)
