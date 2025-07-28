#Create version file in SPIFFS image

```
set(PROJECT_NAME "some_project")
set(PROJECT_VER "1.0.0b")
set(SPIFFS_PARTITION_NAME "spiffs")
set(SPIFFS_PARTITION_DIR "spiffs_data")

set(OUTPUT_NAME "${PROJECT_NAME}_${PROJECT_VER}")

project(${PROJECT_NAME})

spiffs_create_partition_image(${SPIFFS_PARTITION_NAME} ${SPIFFS_PARTITION_DIR} FLASH_IN_PROJECT)

# Custom target to create version.txt in the SPIFFS partition dir before creating the partition image
add_custom_target(write_spiffs_version_file
    COMMAND ${CMAKE_COMMAND} -E make_directory ${SPIFFS_PARTITION_DIR}
    COMMAND ${CMAKE_COMMAND} -E echo "${OUTPUT_NAME}_${SPIFFS_PARTITION_NAME}.bin" > ${CMAKE_BINARY_DIR}/../${SPIFFS_PARTITION_DIR}/version.txt
    COMMENT "Writing version.txt to SPIFFS partition directory"
)
```
