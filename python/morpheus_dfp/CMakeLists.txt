# SPDX-FileCopyrightText: Copyright (c) 2021-2024, NVIDIA CORPORATION & AFFILIATES. All rights reserved.
# SPDX-License-Identifier: Apache-2.0
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

list(APPEND CMAKE_MESSAGE_CONTEXT "morpheus_dfp")

# Save the root of the python for relative paths
set(MORPHEUS_DFP_PY_ROOT ${CMAKE_CURRENT_SOURCE_DIR}/..)


# #####################################
# #### Morpheus DFP Python Setup ######
# #####################################
morpheus_utils_python_configure()

morpheus_utils_create_python_package(morpheus_dfp
  PROJECT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
  SOURCE_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/morpheus_dfp"
)

if(MORPHEUS_PYTHON_INPLACE_BUILD)
  list(APPEND extra_args "IS_INPLACE")
endif()

if(MORPHEUS_PYTHON_BUILD_WHEEL)
  list(APPEND extra_args "BUILD_WHEEL")
endif()

if(MORPHEUS_PYTHON_PERFORM_INSTALL)
  list(APPEND extra_args "INSTALL_WHEEL")
endif()

file(GLOB morpheus_dfp_requirement_files "${CMAKE_CURRENT_SOURCE_DIR}/morpheus_dfp/requirements*")
morpheus_utils_add_python_sources(${morpheus_dfp_requirement_files})

morpheus_utils_build_python_package(morpheus_dfp ${extra_args})

list(POP_BACK CMAKE_MESSAGE_CONTEXT)
