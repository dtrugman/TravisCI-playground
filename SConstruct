# Copyright 2016 Daniel Trugman
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

import platform

# -----------------------------------------------------------------------------
# Set environment
# -----------------------------------------------------------------------------
env=Environment(CPPPATH = '',
                CPPDEFINES = [],
                LIBS = [],
                CXXFLAGS = [])

platform = platform.system()
print("Compiling on: " + platform)

if platform == 'Linux':
    env.Append(LIBS = [ 'pthread' ])
    env.Append(CXXFLAGS = [ '-std=c++11' ])

# -----------------------------------------------------------------------------
# Build flags
# -----------------------------------------------------------------------------

# Default values
DEFAULT_DEBUG = 0 # Debugging off

# Debug flag
debug = ARGUMENTS.get('debug', DEFAULT_DEBUG)
if int(debug):
   env.Append(CXXFLAGS = [ '-g' ])

# Compiler flag
compiler = ARGUMENTS.get('cxx', "")
if compiler:
    env.Replace(CXX = compiler)
print("Compiling using: " + env['CXX'])

# -----------------------------------------------------------------------------
# Build test
# -----------------------------------------------------------------------------
test_files = [ 'TestMain.cpp', 'Test.cpp' ]
test_app = 'Test'

test = env.Program(target = test_app,
                   source = test_files)

test_alias = Alias('test', [test], test[0].abspath)
AlwaysBuild(test_alias)
