# hiera-yaml_hierarchy_expander

Hiera backend plugin that expands the hierarchy definition by interpolating arrays and wildcards.


## Example

```yaml
:backends:
  - yaml_hierarchy_expander

:logger: console

:hierarchy:
  - 'nodes/%{::fqdn}'
  - 'groups/%{::groups}'
  - 'common/*'

:yaml_hierarchy_expander:
  :datadir: '/etc/puppet/environments/%{::environment}/hieradata'
  :expanders: ['::groups']
```

This example shows the two features of the backend:
 - `common/*` is expanded to as much hierarchy lines as yaml files found
 in the `common/` subdirectory
 - `::groups` is an array, and since it is declared in the `:expanders:` section,
 it is expanded to a hierarchy line per item in the array


## License

MIT License, see LICENSE file.


## Contact

Use contact form at http://sbit.io


## Support

Please log tickets and issues on [GitHub](https://github.com/sbitio/hiera-yaml_hierarchy_expander)

