# TMPS_LabN3
### Java version 8 update 201 (Build 1.8.0_201-b09)
*Command, Memento, Observer, State, Mediator.*
___
It is a laboratory work by number 3, where 5 template have been used.
The conception of the project:
We have have a Command pattern as main way to work with the Observer class.
Command class works has a class ExecutableClass with method run, other classes are extended from it, with overrided method 'run'. So it means we can send those classes to method which need as params ExecutableClass. Doing by this we can easily create an Array List where we can save all the commands we need, and execute them than we need it.

```
    ArrayList<Command.ExecCommand> commandArrayList = new ArrayList<>();

    commandArrayList.add(new Command.SubscribeCommand(0, "Johny", "01.02.1994", "Mobile App"));
    commandArrayList.add(new Command.SubscribeCommand(1, "Kate", "11.03.1992", "Mobile App"));
    commandArrayList.add(new Command.SubscribeCommand(erwin));

    for (Command.ExecCommand command : commandArrayList) {
        command.run();
    }
```
This leads us to another pattern - Memento!
Memento gives us save state of Array List of commands and restore it if we need.

```
    Memento.Backup.makeOneBackup(commandArrayList);
    commandArrayList = Memento.Backup.getBackup(0);
```
Observer class implements 'observer' pattern where this class has Array List of Subscribers and has a method for sending messages for every subscriber. Work with this class goes by using State class which implements 'state' pattern.

State has multiple classes which extends class 'state', by doing this i also implement 'composite' pattern. Every state class has methods run() and by switching state class we are also switching and executable code.

Example:
```
    State.Runnable runnableState = new State.Runnable();
    runnableState.setState(new State.PrintAllSubscribers());
    runnableState.run(Observer.InfoCenter.getArrayList());

    runnableState.setState(new State.PrintSize());
    runnableState.run(Observer.InfoCenter.getArrayList());

    runnableState.setState(new State.PrintAllSubscribersAdvanced());
    runnableState.run(Observer.InfoCenter.getArrayList());
```

Example of code:
```
    ArrayList<Command.ExecCommand> commandArrayList = new ArrayList<>();

    commandArrayList.add(new Command.SubscribeCommand(0, "Johny", "01.02.1994", "Mobile App"));
    commandArrayList.add(new Command.SubscribeCommand(1, "Kate", "11.03.1992", "Mobile App"));
    Observer.SubUser erwin = new Observer.SubUser(22, "Erwin", "01.02.1990", "Browser");
    commandArrayList.add(new Command.SubscribeCommand(erwin));


    Memento.Backup.makeOneBackup(commandArrayList);
    Memento.Backup.getInfoAboutOneBackup(Memento.Backup.execCommands.size() - 1);

    commandArrayList.add(new Command.UnsubscribeCommand(0));
        commandArrayList.add(new Command.UnsubscribeCommand(erwin));

    Memento.Backup.makeOneBackup(commandArrayList);
    Memento.Backup.getInfoAboutOneBackup(Memento.Backup.execCommands.size() - 1);

    commandArrayList = Memento.Backup.getBackup(0);

    for (Command.ExecCommand command : commandArrayList) {
        command.run();
    }


    Observer.InfoCenter.sendMessages();


    State.Runnable runnableState = new State.Runnable();
    runnableState.setState(new State.PrintAllSubscribers());
    runnableState.run(Observer.InfoCenter.getArrayList());

    runnableState.setState(new State.PrintSize());
    runnableState.run(Observer.InfoCenter.getArrayList());

    runnableState.setState(new State.PrintAllSubscribersAdvanced());
    runnableState.run(Observer.InfoCenter.getArrayList());
    }
```
