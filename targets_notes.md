# Targets Notes

<!-- targets_notes.md is generated from targets_notes.qmd - edit that file -->

Notes about using the `targets` R package, focused on a few useful
functions and options. For a comprehensive reference, see the {targets}
user manual: <https://books.ropensci.org/targets/>

## visualize / validate the pipeline

- view the network: `tar_visnetwork()`
- see a list of the targets: `tar_manifest()`
- view a simplified network (without functions): `tar_glimpse()`

## run pipeline / clear results

- run the pipeline: `tar_make()`
- invalidate a particular target, to force it to re-run (regardless of
  its actual state): `tar_invalidate()`
- invalidate all targets to force the entire pipeline to re-run (note
  that this does not destroy the `_targets.R` file, just the outputs in
  the `_targets` folder): `tar_destroy()`

## inspect outputs

These functions allow you to view or load the output object from any
target (e.g., a dataset). Before using any of these functions, make sure
to load any packages required to use the given object/dataset (e.g., if
the target object being retrieved is geospatial data, load the `sf`
package - otherwise you’ll get an error when you try to use that
object):

- read an object/target directly (don’t load as a variable):
  `tar_read()`
- load an object/target (as a variable in the global environment):
  `tar_load()`

## debugging / development

Use workspaces:

- save a particular workspace: `tar_option_set(workspaces = c(...))`
- save a workspace for any target that has an error:
  `tar_option_set(workspace_on_error = TRUE)`
- to load a workspace, call: `tar_workspace(workspace_name)`
- to see available workspaces, call: `tar_workspaces()`

## build reports / presentations

- Quarto: `tarchetypes::tar_quarto()`
  - embed target objects (e.g., plots) with
    `targets::tar_read(target_name)`
  - may also want to include
    `store = here::here(tar_config_get('store')))` in the
    `targets::tar_read()` call - this should allow for manual rendering
    (i.e. without having to render using `tar_make()` each time) (might
    not be the best practice though?)
  - make sure packages needed to render the document are included in the
    .qmd file itself (and not just called by `tar_option_set()` in the
    `_targets.R` file)
- Rmarkdown: `tarchetypes::tar_render()`
