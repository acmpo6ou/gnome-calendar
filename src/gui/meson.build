subdir('calendar-management')
subdir('event-editor')
subdir('gtk')
subdir('icons')
subdir('importer')
subdir('views')

calendar_incs +=  include_directories('.')

built_sources += gnome.compile_resources(
  'gui-resources',
  'gui.gresource.xml',
  c_name: 'gui',
)

sources += files(
  'gcal-application.c',
  'gcal-calendar-popover.c',
  'gcal-event-popover.c',
  'gcal-event-widget.c',
  'gcal-expandable-entry.c',
  'gcal-meeting-row.c',
  'gcal-quick-add-popover.c',
  'gcal-search-button.c',
  'gcal-window.c',
)
