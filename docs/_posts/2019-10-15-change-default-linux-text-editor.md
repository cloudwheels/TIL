# Change default Linux text editor to prefered installed program

e.g. change default to `nano`

Add following to ~/.bashrc

```
export EDITOR=nano
export VISUAL=nano
```

Close / reopen terminal OR run 

`$ source ~/.bashrc`

Check environment variable using 

`$ printenv | grep EDITOR`
