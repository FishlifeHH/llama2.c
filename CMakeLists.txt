add_executable(run run.cpp)
target_link_libraries(run m libmyperf papi)
target_link_libraries(run PRIVATE $<TARGET_OBJECTS:common_objs>)
target_link_libraries(run PUBLIC OpenMP::OpenMP_CXX)
