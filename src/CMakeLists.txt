set (quake_resource_libdir /usr/local/lib/quake2sdl)
set (quake_resource_datadir /usr/local/share/quake2)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/q_resources.h.in ${CMAKE_CURRENT_BINARY_DIR}/q_resources.h)

include_directories (${SDL2_INCLUDE_DIR} ${CMAKE_CURRENT_BINARY_DIR})

set (Q2_SOURCES
  client/cl_cin.c
  client/cl_ents.c
  client/cl_input.c
  client/cl_inv.c
  client/cl_main.c
  client/cl_parse.c
  client/cl_pred.c
  client/cl_tent.c
  client/cl_scrn.c
  client/cl_view.c
  client/cl_newfx.c
  client/console.c
  client/keys.c
  client/menu.c
  client/snd_dma.c
  client/snd_mem.c
  client/snd_mix.c
  client/qmenu.c
  game/m_flash.c

  qcommon/cmd.c
  qcommon/cmodel.c
  qcommon/common.c
  qcommon/crc.c
  qcommon/cvar.c
  qcommon/files.c
  qcommon/md4.c
  qcommon/net_chan.c
  qcommon/pmove.c

  server/sv_ccmds.c
  server/sv_ents.c
  server/sv_game.c
  server/sv_init.c
  server/sv_main.c
  server/sv_send.c
  server/sv_user.c
  server/sv_world.c

  linux/q_shlinux.c
  linux/vid_menu.c
  linux/vid_so.c
  linux/sys_linux.c
  linux/glob.c
  linux/net_udp.c
  game/q_shared.c
  linux/snd_sdl.c
)

set (Q2_SOURCES ${Q2_SOURCES} client/cl_fx.c)
add_executable (quake2 ${Q2_SOURCES})
target_link_libraries (quake2 dl SDL2 pthread gfx gui c m)

add_library (ref-softsdl SHARED
  ref_soft/r_aclip.c
  ref_soft/r_alias.c
  ref_soft/r_bsp.c
  ref_soft/r_draw.c
  ref_soft/r_edge.c
  ref_soft/r_image.c
  ref_soft/r_light.c
  ref_soft/r_main.c
  ref_soft/r_misc.c
  ref_soft/r_model.c
  ref_soft/r_part.c
  ref_soft/r_poly.c
  ref_soft/r_polyse.c
  ref_soft/r_rast.c
  ref_soft/r_scan.c
  ref_soft/r_sprite.c
  ref_soft/r_surf.c
  game/q_shared.c
  linux/q_shlinux.c
  linux/glob.c
  linux/rw_linux.c
  linux/rw_sdl.c
  )
set_target_properties (ref-softsdl PROPERTIES OUTPUT_NAME ref_softsdl PREFIX "")

add_library (game-base SHARED
  game/g_ai.c
  game/p_client.c
  game/g_chase.c
  game/g_cmds.c
  game/g_svcmds.c
  game/g_combat.c
  game/g_func.c
  game/g_items.c
  game/g_main.c
  game/g_misc.c
  game/g_monster.c
  game/g_phys.c
  game/g_save.c
  game/g_spawn.c
  game/g_target.c
  game/g_trigger.c
  game/g_turret.c
  game/g_utils.c
  game/g_weapon.c
  game/m_actor.c
  game/m_berserk.c
  game/m_boss2.c
  game/m_boss3.c
  game/m_boss31.c
  game/m_boss32.c
  game/m_brain.c
  game/m_chick.c
  game/m_flipper.c
  game/m_float.c
  game/m_flyer.c
  game/m_gladiator.c
  game/m_gunner.c
  game/m_hover.c
  game/m_infantry.c
  game/m_insane.c
  game/m_medic.c
  game/m_move.c
  game/m_mutant.c
  game/m_parasite.c
  game/m_soldier.c
  game/m_supertank.c
  game/m_tank.c
  game/p_hud.c
  game/p_trail.c
  game/p_view.c
  game/p_weapon.c
  game/q_shared.c
  game/m_flash.c)
set_target_properties (game-base PROPERTIES OUTPUT_NAME gamei386 PREFIX "")

install (TARGETS quake2 RUNTIME DESTINATION bin)
install (TARGETS ref-softsdl LIBRARY DESTINATION lib/quake2sdl)
install (TARGETS game-base LIBRARY DESTINATION lib/quake2sdl/baseq2)
