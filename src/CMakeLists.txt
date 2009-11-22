find_package(PkgConfig)
pkg_check_modules(GOBJECT REQUIRED gobject-2.0)
pkg_check_modules(GIO REQUIRED gio-2.0)
pkg_check_modules(POPPLER REQUIRED poppler-glib)
pkg_check_modules(GTK REQUIRED gtk+-2.0)
pkg_check_modules(GTHREAD REQUIRED gthread-2.0)

set(CFLAGS
	${GOBJECT_CFLAGS} ${GOBJECT_CFLAGS_OTHER}
	${GIO_CFLAGS} ${GIO_CFLAGS_OTHER}
	${POPPLER_CFLAGS} ${POPPLER_CFLAGS_OTHER}
	${GTK_CFLAGS} ${GTK_CFLAGS_OTHER}
	${GTHREAD_CFLAGS} ${GTHREAD_CFLAGS_OTHER}
)
add_definitions(${CFLAGS})

set(LIBS
	${GOBJECT_LIBRARIES}
	${GIO_LIBRARIES}
	${POPPLER_LIBRARIES}
	${GTK_LIBRARIES}
	${GTHREAD_LIBRARIES}
)
link_libraries(${LIBS})

set(VALA_SRC
	pdf_presenter_console.vala
	classes/pdf_image.vala
	classes/presentation_window.vala
	classes/presentation_controller.vala
	classes/presenter_window.vala
	classes/cache_status.vala
)

vala_precompile(VALA_C
	${VALA_SRC}
PACKAGES 
	gio-2.0
	poppler-glib
	gtk+-2.0
	posix
OPTIONS 
	--thread
)

add_executable(pdf_presenter_console ${VALA_C})