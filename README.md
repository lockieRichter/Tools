# Tools

Helpful tools for development.

## Force git prompt to be coloured

To get a coloured git prompt in your terminal add the following to your `.bashrc`.

```bash
force_color_prompt=yes

if [ "$color_prompt" = yes ]; then
    PS1='\[\e[0;32m\][\w]\[\e[35m\]$(__git_ps1 " (%s)")\[\e[37m\] \[\e[0m\]'
else
    PS1='\[\e[0;32m\][\w]$(__git_ps1 " (%s)") \[\e[0m\]'
fi
```

## Redirect output for testing java

Here is some code I use to redirect the standard output for testing in Java.

```java
import java.io.ByteArrayOutputStream;
import java.io.PrintStream;

public class Driver {
    public static void main(String[] args) {
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
    PrintStream output = new PrintStream(baos);

    // Store the old output for later
    PrintStream stdOut = System.out;

    // Set the new output
    System.setOut(output);

    // Do stuff with output
    System.out.println("Hello world!");

    // Print output as string
    System.err.println(baos.toString());

    // Restore standard output
    System.setOut(stdOut);
    }
}
```

## Estimation

Here is a nice method for estimating the time required to do a task or something similar.

When estimating a task provide three estimates.

O: Optimistic Estimate

This is a wildly optimistic estimate, essentially the amount of time it would take if absolutely nothing went wrong.

N: Nominal Estimate

This is the estimate with the greatest chance of success.

P: Pessimistic Estimate

This is the estimate that is wildly pessimistic, essentially the amount of time if almost everything went wrong.

The amount of time the task will take is T = (O + 4N + P) / 6.

The amount of uncertainty of the task is U = (P - O) / 6. The higher this number is the more likely it is that the estimate will be inaccurate.

## Find and replace a string through terminal

```bash
grep -rl <word to be replaced> | xargs sed -i 's/<word to be replaced>/<new word to replace>/g'
```

for example

```bash
grep -rl testjunit | xargs sed -i 's/testjunit/test1/g'
```

NOTE: The -rl flag on grep will make it search recursively, so this will search current directory and ALL directories.

## Rename a git branch locally and remotely

```bash
git branch -m old_branch new_branch #This step will only do local if you so choose
git push origin :old_branch
git push --set-upstream origin new_branch
```

## Aliases

I like to use the `.aliases` file to store my useful aliases.
Set the aliases in the following ways.

.bashrc:

```bash
if [ -f ~/.aliases ]; then
    . ~/.aliases
fi
```

.zshrc:

```zsh
source $HOME/.aliases
```
