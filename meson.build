project(
    'io.elementary.appcenter',
    'vala', 'c',
    version: '3.4.0'
)

gettext_name = meson.project_name()
gnome = import('gnome')
i18n = import('i18n')

add_project_arguments(
    '-DGETTEXT_PACKAGE="@0@"'.format(gettext_name),
    '-DHANDY_USE_UNSTABLE_API',
    '-DI_KNOW_THE_PACKAGEKIT_GLIB2_API_IS_SUBJECT_TO_CHANGE',
    language:'c'
)

vapi_dir = join_paths(meson.current_source_dir(), 'vapi')
add_project_arguments(['--vapidir', vapi_dir], language: 'vala')

glib = dependency ('glib-2.0')
gee = dependency ('gee-0.8')
gtk = dependency ('gtk+-3.0', version: '>=3.10')
granite = dependency ('granite', version: '>=5.2.5')
handy = dependency('libhandy-0.0', version: '>=0.0.11')
packagekit = dependency ('packagekit-glib2')
appstream = dependency ('appstream', version: '>=0.10.0')
libsoup = dependency ('libsoup-2.4')
json = dependency ('json-glib-1.0')
flatpak = dependency ('flatpak')
xml = dependency ('libxml-2.0')
polkit = dependency ('polkit-gobject-1')
posix = meson.get_compiler('vala').find_library('posix')

dbus = dependency ('dbus-1')

dependencies = [
    glib,
    gee,
    gtk,
    granite,
    handy,
    packagekit,
    appstream,
    libsoup,
    json,
    flatpak,
    xml,
    polkit,
    posix
]

config_dir = join_paths(get_option('sysconfdir'), meson.project_name())
conf_data = configuration_data()
conf_data.set('PROJECT_NAME', meson.project_name())
conf_data.set('DESKTOP_ICON', get_option('icon'))
conf_data.set('EXEC_NAME', meson.project_name())
conf_data.set('GETTEXT_PACKAGE', meson.project_name())
conf_data.set('APP_NAME', get_option('name'))
conf_data.set('HIDDEN_APP_LIST', get_option('hidden_app_list_file'))
conf_data.set('VERSION', meson.project_version())
conf_data.set('CONFIGDIR', config_dir)
conf_data.set('EXEC_PATH', join_paths (get_option('prefix'), get_option('bindir'), meson.project_name()))
conf_data.set('HOUSTON_API_URL', get_option('api_url'))

subdir('data')
subdir('src')
subdir('po')

meson.add_install_script('meson/post_install.py')
