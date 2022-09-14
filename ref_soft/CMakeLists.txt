
set(SOURCES_REF_SOFT
./adivtab.h
./anorms.h
./r_aclip.c
./r_alias.c
./r_bsp.c
./r_draw.c
./r_edge.c
./r_image.c
./r_light.c
./r_local.h
./r_main.c
./r_misc.c
./r_model.c
./r_model.h
./r_part.c
./r_poly.c
./r_polyse.c
./r_rast.c
./r_scan.c
./r_sprite.c
./r_surf.c
./rand1k.h
)

set(SOURCES_REF_SOFT_ASM
./r_aclipa.asm
./r_draw16.asm
./r_drawa.asm
./r_edgea.asm
./r_polysa.asm
./r_scana.asm
./r_spr8.asm
./r_surf8.asm
./r_varsa.asm
)

set(SOURCES_CLIENT
../client/ref.h
)

set(SOURCES_GAME
../game/q_shared.c
../game/q_shared.h
)

set(SOURCES_QCOMMON
../qcommon/qcommon.h
../qcommon/qfiles.h
)


set(SOURCES ${SOURCES_REF_SOFT} ${SOURCES_CLIENT} ${SOURCES_GAME} ${SOURCES_QCOMMON})
set(RESOURCES )

set(SOURCES_WIN32
../win32/q_shwin.c
../win32/rw_ddraw.c
../win32/rw_dib.c
../win32/rw_imp.c
../win32/rw_win.h
../win32/winquake.h
)

set(RESOURCES_WIN32
./ref_soft.def
)

if(WIN32)
    set(RESOURCES ${RESOURCES} ${RESOURCES_WIN32})
    set(SOURCES ${SOURCES} ${SOURCES_WIN32})
    add_library(ref_soft SHARED ${SOURCES} ${RESOURCES})
    target_link_libraries(ref_soft Winmm)
endif()