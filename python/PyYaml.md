# Py YAML
PyYaml is useful library for creating or editing a YAML file.

## ignore_aliases
YAML document supports the pointer concepts, so if there are any duplicate blocks it will define the first block and assign a pointer value and the other occurences uses the pointer value. It is a valid YAML but sometimes we prefer to use the block as it is instead of using pointer.

In order to avoid using the pointer, we need to configure the YAML dumper with *ignore_aliases*

```
# -------------------------------------------------------------
# This helper function disables the use of aliases in yaml dump
# If the aliases is enabled then in the generated yaml
# will avoid the duplications and uses pointer
# -------------------------------------------------------------
def _get_dumper_settings():
    noalias_dumper = yaml.dumper.SafeDumper
    noalias_dumper.ignore_aliases = lambda self, data: True
    return noalias_dumper

# Whereever we want to skip aliases, we should use the above dumper
yaml.dump(content, f, default_flow_style=False, Dumper=_get_dumper_settings())
```   

 