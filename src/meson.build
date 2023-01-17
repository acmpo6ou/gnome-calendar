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

libgcal = shared_library('gcal',
              sources: sources,
  include_directories: calendar_incs,
         dependencies: gcal_deps,
)

headers_gir = files(
  'core/gcal-time-zone-monitor.h',
  'core/gcal-recurrence.h',
  'gui/gcal-calendar-popover.h',
  'gui/calendar-management/gcal-edit-calendar-page.h',
  'gui/css-code.h',
  'gui/views/gcal-week-grid.h',
  'core/gcal-timeline.h',
  'gui/event-editor/gcal-event-editor-dialog.h',
  'search/gcal-search-hit-event.h',
  'gui/event-editor/gcal-alarm-row.h',
  'gui/importer/gcal-import-file-row.h',
  'gcal-enums.h',
  'gui/event-editor/gcal-date-chooser-day.h',
  'gui/calendar-management/gcal-calendars-page.h',
  'gui/gcal-window.h',
  'gui/event-editor/gcal-reminders-section.h',
  'core/gcal-event.h',
  'utils/gcal-date-time-utils.h',
  'core/gcal-clock.h',
  'gconstructor.h',
  'gui/gcal-meeting-row.h',
  'gui/views/gcal-view.h',
  'gui/views/gcal-week-header.h',
  'weather/gcal-weather-service.h',
  'gui/gcal-search-button.h',
  'core/gcal-manager.h',
  'gui/event-editor/gcal-schedule-section.h',
  'gui/event-editor/gcal-summary-section.h',
  'gui/views/gcal-year-view.h',
  'gui/gcal-event-widget.h',
  'gui/views/gcal-month-cell.h',
  'gui/gcal-weather-settings.h',
  'core/gcal-timeline-subscriber.h',
  'gui/importer/gcal-importer.h',
  'gui/event-editor/gcal-time-selector.h',
  'search/gcal-search-hit.h',
  'gui/event-editor/gcal-date-chooser.h',
  'core/gcal-timer.h',
  'gui/gcal-quick-add-popover.h',
  'search/gcal-search-model.h',
  'gcal-types.h',
  'gui/gcal-expandable-entry.h',
  'gui/gcal-event-popover.h',
  'gui/calendar-management/gcal-calendar-management-page.h',
  'gui/calendar-management/gcal-calendar-management-dialog.h',
  'core/gcal-calendar.h',
  'core/gcal-shell-search-provider.h',
  'gui/calendar-management/gcal-new-calendar-page.h',
  'gui/event-editor/gcal-multi-choice.h',
  'utils/gcal-source-discoverer.h',
  'gui/event-editor/gcal-event-editor-section.h',
  'gui/gcal-application.h',
  'gui/event-editor/gcal-notes-section.h',
  'utils/gcal-utils.h',
  'core/gcal-night-light-monitor.h',
  'search/gcal-search-engine.h',
  'core/gcal-context.h',
  'core/gcal-log.h',
  'gui/views/gcal-week-view.h',
  'gui/event-editor/gcal-date-selector.h',
  'gui/views/gcal-month-popover.h',
  'gui/importer/gcal-import-dialog.h',
  'core/gcal-range-tree.h',
  'weather/gcal-weather-info.h',
  'core/gcal-range.h',
  'core/gcal-calendar-monitor.h',
  'gui/views/gcal-month-view.h',
)

gnome = import('gnome')
gnome.generate_gir(libgcal,
  sources: [sources, headers_gir],
  namespace: 'Gcal',
  nsversion: '1.0',
  identifier_prefix: 'Gcal',
  dependencies: gcal_deps,
  symbol_prefix: 'gcal',
  includes: ['Handy-1', 'Soup-2.4', 'ICal-3.0', 'Dazzle-1.0', 'ECal-2.0', 'EDataServer-1.2', 'EDataServerUI-1.2', 'GLib-2.0', 'Gtk-3.0', 'Gio-2.0', 'Goa-1.0', 'GWeather-3.0', 'Geoclue-2.0', 'GeocodeGlib-1.0'],
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
