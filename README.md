# hiera-yaml_hierarchy_expander

Hiera backend plugin that expands the hierarchy definition by interpolating arrays and wildcards.


## *This module is deprecated in Puppet > 4.9 / Hiera 5*

Happily, Hiera 5 provides (almost) the same functionality as this extension,
so our recomendation is to upgrade and stop using `yaml_hierarchy_expander`.

See [Hiera: Config file syntax](https://puppet.com/docs/puppet/4.10/hiera_config_yaml_5.html) for details.

In a brief, here's the correspondence between `yaml_hierarchy_expander` config and the Hiera 5 equivalent.

```
# yaml_hierarchy_expander

:hierarchy:
  - 'groups/%{::groups}'
  - 'common/*'

# hiera 5

hierarchy:
  - name: Per group data files
    mapped_paths: [facts.groups, group, "groups/%{group}.yaml"]

  - name: Common data data glob
    glob: "common/*.yaml"
```

The only feature not covered by Hiera 5 is a mix of array expansion and wildcards like:

```
groups/%{::groups}/*
```

This is a kind of `mapped_globs`, not provided (yet?) by Hiera 5.


## Compatibility

Use 1.x.x releases for Hiera 1.x and 2.x, and 2.x.x releases for Hiera 3.x.

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

