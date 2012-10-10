project( FDesktopRecorder )
cmake_minimum_required( VERSION 2.6 )
set ( CMAKE_BUILD_TYPE Release )
add_definitions ( -Wall )
find_package ( Qt4 REQUIRED )
find_package ( KDE4 REQUIRED) 
include ( ${QT_USE_FILE} ${KDE4Defaults} ${QT_USE_PHONON})
include_directories (
	${CMAKE_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR}
	${QT_QTCORE_INCLUDE_DIR} ${QT_QTGUI_INCLUDE_DIR} ${QT_QTCORE_INCLUDE_DIR} ${QT_QTGUI_INCLUDE_DIR}
	${QT_KDE4_INCLUDE_DIR} ${QT_KDE4_LIBRARY} ${KDE4_INCLUDES} ${KDE4_KDECORE_LIBS}
	)
set ( FDesktopRecorder_HDRS
	
	)

set ( FDesktopRecorder_SRCS
	main.cpp
	mainwindow.cpp
	dialogs/about/aboutprog.cpp
	utils/windowgrapper.cpp
	module/recordingdevices.cpp
	dialogs/settingsdialog/settingsdialog.cpp
	module/process.cpp
	module/settingsmanager.cpp
	utils/rubberband.cpp
	)

set ( FDesktopRecorder_UIS
	mainwindow.ui
	dialogs/about/aboutprog.ui
	dialogs/settingsdialog/settingsdialog.ui
	)
QT4_WRAP_UI(UIS ${FDesktopRecorder_UIS})

set ( FDesktopRecorder_RSCS
        resources.qrc
	)
QT4_ADD_RESOURCES(RSCS ${FDesktopRecorder_RSCS})

set ( FDesktopRecorder_TRS
	translations/FDesktopRecorder.main/da_DK.ts
	translations/FDesktopRecorder.main/de_DE.ts
        translations/FDesktopRecorder.main/it_IT.ts
        translations/FDesktopRecorder.main/ro_RO.ts
	translations/FDesktopRecorder_untranslated.ts
	)
QT4_ADD_TRANSLATION(TRS ${FDesktopRecorder_TRS})

set ( FDesktopRecorder_MOCS
	mainwindow.h
	dialogs/about/aboutprog.h
	utils/windowgrapper.h
	module/recordingdevices.h
	dialogs/settingsdialog/settingsdialog.h
	module/process.h
	module/settingsmanager.h
	utils/rubberband.h
	)
QT4_WRAP_CPP(MOCS ${FDesktopRecorder_MOCS})

add_executable ( FDesktopRecorder ${FDesktopRecorder_SRCS} ${UIS} ${RSCS} ${TRS} ${MOCS} )
target_link_libraries ( FDesktopRecorder  ${QT_QTCORE_LIBRARY} ${QT_QTGUI_LIBRARY} ${QT_QTCORE_LIBRARY} ${QT_QTGUI_LIBRARY} ${KDE4_KDEUI_LIBS} ${KDE4_KPARTS_LIBS} phonon)

# add the install targets
install (TARGETS FDesktopRecorder DESTINATION bin)
install( FILES ../knotification/FDesktopRecorder.notifyrc DESTINATION share/kde4/apps/FDesktopRecorder)
install( FILES ../Desktop/FDesktopRecorder.desktop DESTINATION share/applications/)
install( FILES ../Desktop/fdesktoprecorder.png DESTINATION share/pixmaps/)