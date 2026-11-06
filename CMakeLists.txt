   zephyr_library()
   zephyr_include_directories(include)
   zephyr_library_include_directories(${APPLICATION_SOURCE_DIR}/include)

   # Driver: build on whichever half the trackball is wired to (central OR peripheral)
   zephyr_library_sources_ifdef(CONFIG_ZMK_PIMORONI_PIM447 src/pimoroni_pim447.c src/pimoroni_pim447_led.c)

   # Keymap behaviors only make sense where the keymap runs (central / unibody)
   if ((NOT CONFIG_ZMK_SPLIT) OR CONFIG_ZMK_SPLIT_ROLE_CENTRAL)
     target_sources_ifdef(CONFIG_ZMK_PIM447_BEHAVIORS app PRIVATE src/behaviors/behavior_pim447.c)
   endif()
