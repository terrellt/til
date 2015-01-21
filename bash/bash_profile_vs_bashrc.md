# `.bash_profile` vs `.bashrc`

`.bashrc` is sourced on every interactive shell start. Here are some ways to
start `bash(1)` interactively:

    bash
    bash -i
    bash -ic 'echo Hello!'

`bash(1)` is also started interactively by your terminal emulator.

Here are some ways to start bash in non-interactive mode:

    bash script.sh
    bash -c 'echo Hello!'
    bash --login

`.bash_profile` is only sourced when `bash(1)` is started as an interactive
login shell, or as a non-interactive shell with the `--login` option.

The login shell is started when you login to your machine or when you start
`bash(1)` with the `--login` option.

This means that `.bash_profile` is great for commands that should run only once
and `.bashrc` for commands that should run every time you start a new shell.

For example, `PATH` customization should only happen once, since it is not an
idempotent operation. Suppose something like this was in your `.bashrc`:

    export PATH="$PATH:/addition"

Then running these commands from a newly started interactive shell would produce
the output below:

    bash
    bash
    echo "$PATH"
    /original_path:/addition:/addition:/addition

Setting `PATH` in `.bash_profile` alleviates this problem.
