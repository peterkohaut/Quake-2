cmake_minimum_required(VERSION 3.10)

project(Quake-2)

add_definitions(-DCPUSTRING="x86_64" -DC_ONLY)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)


if(CMAKE_SYSTEM_PROCESSOR STREQUAL "AMD64")
    set(GAME "gamex64")
else()
    set(GAME "gamex86")
endif()

add_subdirectory(ref_gl)
add_subdirectory(ref_soft)
add_subdirectory(game)


set(SOURCES_CLIENT
./client/anorms.h
./client/cdaudio.h
./client/cl_cin.c
./client/cl_ents.c
./client/cl_fx.c
./client/cl_input.c
./client/cl_inv.c
./client/cl_main.c
./client/cl_newfx.c
./client/cl_parse.c
./client/cl_pred.c
./client/cl_scrn.c
./client/cl_tent.c
./client/cl_view.c
./client/client.h
./client/console.c
./client/console.h
./client/input.h
./client/keys.c
./client/keys.h
./client/menu.c
./client/qmenu.c
./client/qmenu.h
./client/ref.h
./client/screen.h
./client/snd_dma.c
./client/snd_loc.h
./client/snd_mem.c
./client/snd_mix.c
./client/sound.h
./client/vid.h
./client/x86.c
)

set(SOURCES_GAME
./game/game.h
./game/m_flash.c
./game/q_shared.c
./game/q_shared.h
)

set(SOURCES_QCOMMON
./qcommon/cmd.c
./qcommon/cmodel.c
./qcommon/common.c
./qcommon/crc.c
./qcommon/cvar.c
./qcommon/files.c
./qcommon/md4.c
./qcommon/net_chan.c
./qcommon/pmove.c
./qcommon/qcommon.h
./qcommon/qfiles.h
)

set(SOURCES_SERVER
./server/server.h
./server/sv_ccmds.c
./server/sv_ents.c
./server/sv_game.c
./server/sv_init.c
./server/sv_main.c
./server/sv_send.c
./server/sv_user.c
./server/sv_world.c
)

set(SOURCES ${SOURCES_CLIENT} ${SOURCES_GAME} ${SOURCES_QCOMMON} ${SOURCES_SERVER})
set(RESOURCES)

set(SOURCES_WIN32
./win32/cd_win.c
./win32/conproc.c
./win32/conproc.h
./win32/in_win.c
./win32/net_wins.c
./win32/q_shwin.c
./win32/snd_win.c
./win32/sys_win.c
./win32/vid_dll.c
./win32/vid_menu.c
./win32/winquake.h
)

set(RESOURCES_WIN32
./win32/q2.ico
./win32/q2.rc
)

if(WIN32)
    set(RESOURCES ${RESOURCES} ${RESOURCES_WIN32})
    set(SOURCES ${SOURCES} ${SOURCES_WIN32})
    add_executable(quake2 WIN32 ${SOURCES} ${RESOURCES})
    target_link_libraries(quake2 wsock32 Winmm)
    add_dependencies(quake2 ref_gl)
    add_dependencies(quake2 ref_soft)
    add_dependencies(quake2 ${GAME})
endif()
