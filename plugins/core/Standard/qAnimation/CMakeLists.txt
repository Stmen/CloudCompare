option( PLUGIN_STANDARD_QANIMATION "Install qAnimation plugin" OFF )

if( PLUGIN_STANDARD_QANIMATION )
	option( QANIMATION_WITH_FFMPEG_SUPPORT "Setup FFMPEG support (to create movies instead of images with qAnimation)" OFF )

	project( QANIMATION_PLUGIN )

	AddPlugin( NAME ${PROJECT_NAME} )

	add_subdirectory( include )
	add_subdirectory( src )
	add_subdirectory( ui )

	if( QANIMATION_WITH_FFMPEG_SUPPORT )
		add_subdirectory( extern/QTFFmpegWrapper ) # Can't use EXCLUDE_FROM_ALL because this lib installs some DLLs

		target_link_libraries( ${PROJECT_NAME} QTFFMPEG_LIB )
		target_compile_definitions( ${PROJECT_NAME} PRIVATE QFFMPEG_SUPPORT )
	endif()
endif()
