src_inc = include_directories('.')

gcal_deps = [
  gsettings_desktop_schemas_dep,
  libedataserverui_dep,
  libedataserver_dep,
  libecal_dep,
  libdazzle_dep,
  libsoup_dep,
  libical_dep,
  libhandy_dep,
  glib_dep,
  gtk_dep,
  gio_dep,
  goa_dep,
  gweather_dep,
  geoclue_dep,
  geocode_dep,
  m_dep,
]

enum_types = 'gcal-enum-types'

built_sources = gnome.mkenums(
  enum_types,
     sources: enum_headers,
  c_template: enum_types + '.c.template',
  h_template: enum_types + '.h.template'
)

built_sources += gnome.gdbus_codegen(
  'gcal-shell-search-provider-generated',
  shell_search_provider_dbus_interfaces,
  interface_prefix: 'org.gnome.',
         namespace: 'Gcal'
)

debug_conf = configuration_data()
debug_conf.set('BUGREPORT_URL', package_bugreport)
debug_conf.set10('ENABLE_TRACING', enable_tracing)


#########
# Debug #
#########

debug = 'gcal-debug.h'

built_sources += configure_file(
          input: debug + '.in',
         output: debug,
  configuration: debug_conf
)


#######################
# Include directories #
#######################

calendar_incs = [
  top_inc,
  include_directories('.'),
]

###################
# Private library #
###################

sources = files()
subdir('core')
subdir('gui')
subdir('search')
subdir('theme')
subdir('utils')
subdir('weather')

libgcal_generated_sources_dep = declare_dependency(
  sources: built_sources,
)

gcal_deps += libgcal_generated_sources_dep

libgcal = library('gcal',
              sources: sources,
  include_directories: calendar_incs,
         dependencies: gcal_deps,
)

headers_gir = files(
  'core/gcal-calendar.h',
  'core/gcal-calendar-monitor.h',
  'core/gcal-clock.h',
  'core/gcal-context.h',
  'core/gcal-event.h',
  'core/gcal-log.h',
  'core/gcal-manager.h',
  'core/gcal-night-light-monitor.h',
  'core/gcal-range.h',
  'core/gcal-range-tree.h',
  'core/gcal-recurrence.h',
  'core/gcal-shell-search-provider.h',
  'core/gcal-timeline.h',
  'core/gcal-timeline-subscriber.h',
  'core/gcal-timer.h',
  'core/gcal-time-zone-monitor.h',
  'gui/calendar-management/gcal-calendar-management-dialog.h',
  'gui/calendar-management/gcal-calendar-management-page.h',
  'gui/calendar-management/gcal-calendars-page.h',
  'gui/calendar-management/gcal-edit-calendar-page.h',
  'gui/calendar-management/gcal-new-calendar-page.h',
  'gui/event-editor/gcal-alarm-row.h',
  'gui/event-editor/gcal-date-chooser.h',
  'gui/event-editor/gcal-date-chooser-day.h',
  'gui/event-editor/gcal-date-selector.h',
  'gui/event-editor/gcal-event-editor-dialog.h',
  'gui/event-editor/gcal-event-editor-section.h',
  'gui/event-editor/gcal-multi-choice.h',
  'gui/event-editor/gcal-notes-section.h',
  'gui/event-editor/gcal-reminders-section.h',
  'gui/event-editor/gcal-schedule-section.h',
  'gui/event-editor/gcal-summary-section.h',
  'gui/event-editor/gcal-time-selector.h',
  'gui/importer/gcal-import-dialog.h',
  'gui/importer/gcal-import-file-row.h',
  'gui/importer/gcal-importer.h',
  'gui/views/gcal-month-cell.h',
  'gui/views/gcal-month-popover.h',
  'gui/views/gcal-month-view.h',
  'gui/views/gcal-view.h',
  'gui/views/gcal-week-grid.h',
  'gui/views/gcal-week-header.h',
  'gui/views/gcal-week-view.h',
  'gui/views/gcal-year-view.h',
  'gui/gcal-application.h',
  'gui/gcal-calendar-popover.h',
  'gui/gcal-event-popover.h',
  'gui/gcal-event-widget.h',
  'gui/gcal-expandable-entry.h',
  'gui/gcal-meeting-row.h',
  'gui/gcal-quick-add-popover.h',
  'gui/gcal-search-button.h',
  'gui/gcal-weather-settings.h',
  'gui/gcal-window.h',
  'search/gcal-search-engine.h',
  'search/gcal-search-hit.h',
  'search/gcal-search-hit-event.h',
  'search/gcal-search-model.h',
  'utils/gcal-date-time-utils.h',
  'utils/gcal-source-discoverer.h',
  'utils/gcal-utils.h',
  'weather/gcal-weather-info.h',
  'weather/gcal-weather-service.h',
)

gnome = import('gnome')
gnome.generate_gir(libgcal,
  sources: [sources, headers_gir],
  namespace: 'Gcal',
  nsversion: '1.0',
  identifier_prefix: 'Gcal',
  dependencies: gcal_deps,
  symbol_prefix: 'gcal',
)

libgcal_dep = declare_dependency(
            link_with: libgcal,
              sources: built_sources,
         dependencies: gcal_deps,
  include_directories: calendar_incs,
)


##################
# gnome-calendar #
##################

#executable(
  #meson.project_name(),
       #files('main.c'),
          #dependencies: libgcal_dep,
               #install: true,
           #install_dir: calendar_bindir,
#)
