project(test C)

macro(postprotoc TARGET FILENAME)
    add_custom_command(
        TARGET ${TARGET} POST_BUILD
        COMMAND protoc -o ${CMAKE_CURRENT_BINARY_DIR}/${FILENAME}.pb ${CMAKE_CURRENT_SOURCE_DIR}/${FILENAME}.proto)
endmacro()
foreach(TESTFILE addressbook pattern pbc float map test decode)
    add_executable(${TESTFILE} ${TESTFILE}.c)
    target_link_libraries(${TESTFILE} libpbc)
endforeach()

postprotoc(addressbook addressbook)
postprotoc(float float)
postprotoc(pattern addressbook)
postprotoc(test test)
