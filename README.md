If I want to cache docker layer:
https://www.blacksmith.sh/blog/cache-is-king-a-guide-for-docker-layer-caching-in-github-actions

If I want to cache python deps:
https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching

What I'm using:
https://github.com/marketplace/actions/ros-2-ci-action

To share the workflow across other repos:
https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows 

Commands
colcon test
colcon test-result --verbose --all

find_package(ament_cmake_cppcheck REQUIRED)
find_package(ament_cmake_lint_cmake REQUIRED)
find_package(ament_cmake_flake8 REQUIRED)
find_package(ament_cmake_pep257 REQUIRED)
find_package(ament_cmake_uncrustify REQUIRED)
find_package(ament_cmake_xmllint REQUIRED)

ament_cppcheck()
ament_lint_cmake()
ament_flake8()
ament_pep257()
ament_uncrustify()
ament_xmllint()


The issue:
I need to run colcon build in order to run colcon test, which makes it hard to test submodules individually. 

If I separate and directly use linters or formatters, they might not have the same configs as what ROS will use. Not too huge an issue

Just make sure colcon build works I guess