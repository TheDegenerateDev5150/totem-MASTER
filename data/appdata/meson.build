source_appdata = 'org.gnome.Totem.appdata.xml'
dest_appdata = application_id + '.appdata.xml'

appdata_in = configure_file(
  input: source_appdata + '.in.in',
  output: source_appdata + '.in',
  configuration: desktop_conf
)

appdata_file = i18n.merge_file (
    input: appdata_in,
    output: dest_appdata,
    install: true,
    install_dir: join_paths(totem_datadir, 'metainfo'),
    po_dir: po_dir,)

# Validate Appdata
appstreamcli = find_program('appstreamcli', required: false)
if appstreamcli.found()
  test(
      'validate-appdata', appstreamcli,
      depends: appdata_file,
      args: ['validate', '--no-net', '--explain', appdata_file.full_path()]
      )
endif
