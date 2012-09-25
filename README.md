# slurm.el

`slurm.el` is an Emacs extension allowing to work more easily with the
[SLURM](https://computing.llnl.gov/linux/slurm/) job scheduling system.

It is composed of two parts:

1. `slurm-script-mode`: a minor mode to edit job submission scripts;
2. `slurm-mode`: a major mode allowing interaction with SLURM.



## Installation

Just put the following lines in your Emacs initialization file (`.emacs` or `.emacs.d/init.el`):

    (add-to-list 'load-path "/path/to/slurm.el")
    (require 'slurm)



## `slurm-script-mode`

`slurm-script-mode` is automatically activated for shell-scripts containing `#SBATCH` directives. It
can also be manually toggled by running `M-x slurm-script-mode`.

While in this mode, `#SBATCH` directives are highlighted. New directives can also be easily inserted
using the `C-c C-d` binding, which proposes completion on the keywords.



## `slurm-mode`

### Basic usage

Just run `M-x slurm` to see a list of all SLURM jobs on the cluster.

`slurm.el` defines several views to present SLURM information. Each view first presents the command
line which have been used to obtain the information presented.

In all views, the following bindings are available:

- `h`: show **h**elp
- `g`: refresh view

   
#### Views

The following key bindings can be used to switch between views:

- `j`: **j**obs list (default view)
- `p`: **p**artitions list
- `i`: cluster **i**nformation


#### Jobs list

This view displays the list of all jobs managed by SLURM on the cluster, as obtained with the
`squeue` command.

The jobs list can be manipulated using the following bindings:

- `/`: filter the jobs list by:
  - `u`: **u**ser;
  - `p`: **p**artition.

- `s`: sort the jobs list by:
  - `u`: **u**ser;
  - `p`: **p**artition;
  - `P`: job **p**riority;
  - `d`: use the **d**efault sorting order;
  - `c`: **c**ustomize sorting order by specifying a suitable argument for the `-S` switch of `squeue`.

  Giving this command a prefix argument reverses the sorting order. For example, `C-u s u` sorts by
  user in reverse alphabetical order.


A few operations can be done from this view:

- `RET`: show job details, as obtained with the `scontrol show job JOBID` command.

- `U`: show **u**ser details on the job submitter (using the `finger USER` command).

- `k` or `d`: **k**ill job by issuing the `scancel JOBID` command.

- `e` or `u`: **e**dit (or **u**pdate) job.

   In this mode, job submission parameters can be interactively updated (as could be done using the
   `scontrol update job JOBID` command). Each parameter is presented on its own line. After editing
   a line, pressing
   - `C-c C-c` validates the changes (on the current line only), or
   - `C-c C-q` cancels the changes and returns to the previous view.


#### Partitions list

This view displays a list of all partitions on the cluster, as obtained with the `scontrol show
partition` command.

While in this view, pressing `RET` allows you to access various details about the selected partition
state, as obtained using the `sinfo` command.

#### Cluster information

This view displays details on the current cluster state, as obtained with the `sinfo` command.


### Customization

Some variables can be set to customize `slurm-mode`'s behaviour:

- `slurm-display-help`: if non-nil, `slurm-mode` displays an help message at the top of the
  screen;

- `slurm-filter-user-at-start`: if non-nil, the initial jobs list is filtered to show only jobs
  owned by the current user.

- `slurm-script-directive-face`: face name to use for `#SBATCH` directives in job submission
  scripts.
  
All these variables can be customized via `M-x customize-group RET slurm RET`.


## Contributing

If you make improvements to this code or have suggestions, please do not hesitate to fork the
repository or submit bug reports on [github](https://github.com/ffevotte/slurm.el). The repository's
URL is:

    https://github.com/ffevotte/slurm.el.git
    
`slurm-script-mode.el` originally comes from the
[slurm-helper](https://github.com/damienfrancois/slurm-helper/blob/master/slurm-mode.el) project by
Damien François.

## License

Copyright (C) 2012 François Févotte, Damien François.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU
General Public License as published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without
even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not,
see <http://www.gnu.org/licenses/>.
