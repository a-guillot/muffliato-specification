# Muffliato specification

This specification was done using the model checker [nuXmv](https://nuxmv.fbk.eu/).
The security properties are specified using Linear Temporal Logic (LTL).

## Structure of the model

The model is organized as follows:

- `task_init.smv`: Contains the information about the bootstrap of the workflow. The variables exchanged during the preparation step are already present, and are used by the Workflow Controller to configure the different entities.
- `task_inter.smv`: Models how data is exchanged between the different tasks. Here, 2 podouts transfer the outputs of their tasks to another task which will process them.
- `task_intra.smv`: Models the inner-workings of a task. It starts with data arriving, and transitions all the way to the completion of the task.

## Launching the model

The files described above are executed using the following command:

```
    reset; read_model -i FILENAME; go; pick_state; simulate -p
```

The output displays one of the possible executions.

## Verifying the properties on the model

To verify that our properties are verified for all possible executions, we check if our LTL properties are verified. We achieve this with the following command:

```
    reset; read_model -i FILENAME; go; pick_state; simulate; check_ltlspec;
```