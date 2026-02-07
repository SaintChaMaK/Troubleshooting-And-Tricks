### Important details to know: -
###### ComputerName
To add a Computer to the Active Directory(AD) in window server we need to know the name of the computer (MacOs ComputerName that we want to add).
Running command such as scutil --get ComputerName on your Mac Terminal will display the CompterName of your Mac Pc.

```
scutil --get ComputerName
```

If you get some problems regarding the name you can rename it using command

```
sudo scutil --set ComputerName ["NewNameOfComputerThatYouWantToNameIt"]
```

for consistent if you decide to change the ComputerName change also the LocalHostName and HostName(Optional), using the same command.

```
sudo scutil --set LocalHostName ["NewNameOfComputerThatYouWantToNameIt"]
```

```
sudo scutil --set HostName ["NewNameOfComputerThatYouWantToNameIt"].localdomain
```




Youtube tutorials on how to add MacOs into an Active Directory

https://www.youtube.com/watch?v=2ad1qTdMiMY

https://www.youtube.com/watch?v=jHqY2txtQ0k
