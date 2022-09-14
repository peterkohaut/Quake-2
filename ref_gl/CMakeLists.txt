
set(SOURCES_REF_GL
./anorms.h
./anormtab.h
./gl_draw.c
./gl_image.c
./gl_light.c
./gl_local.h
./gl_mesh.c
./gl_model.c
./gl_model.h
./gl_rmain.c
./gl_rmisc.c
./gl_rsurf.c
./gl_warp.c
./qgl.h
./warpsin.h
)

set(SOURCES_CLIENT
../client/qmenu.h
../client/ref.h
)

set(SOURCES_GAME
../game/q_shared.c
../game/q_shared.h
)

set(SOURCES ${SOURCES_REF_GL} ${SOURCES_CLIENT} ${SOURCES_GAME})
set(RESOURCES )

set(SOURCES_WIN32
../win32/glw_imp.c
../win32/glw_win.h
../win32/q_shwin.c
../win32/qgl_win.c
../win32/winquake.h
)

set(RESOURCES_WIN32
./ref_gl.def
)

if(WIN32)
    set(RESOURCES ${RESOURCES} ${RESOURCES_WIN32})
    set(SOURCES ${SOURCES} ${SOURCES_WIN32})
    add_library(ref_gl SHARED ${SOURCES} ${RESOURCES})
    target_link_libraries(ref_gl Winmm)
endif()