# Overview #

While Killing Sprees, Death Sprees, and Multi-kills are configured similarly to each other, but it is important to understand that they are enabled differently.  This behavior is by design to allow server operators/owners the ability to pick and choose what features they want to include.

# Details #

### Killing Sprees and Death Sprees ###

Killing Sprees and Death Sprees are enabled together.  If only one of these features is desired, server owners must specify this in the configuration step.

To enable them, first, the cvar "g\_sprees" must be set to the name of the settings file contained in the working directory for Open Arena.

For example, under Windows, the file would reside under the `%APPDATA%\OpenArena\baseoa` directory (where user name is the name of the user that launches the server.  See the linux documentation at http://openarena.ws/ for the various linux specifications of the "working directory."

So, for the example above setting "g\_sprees" to "sprees.dat" would specify OpenArena to look for `%APPDATA%\OpenArena\baseoa\sprees.dat`.

Next, the cvar "g\_spreeDiv" must be set to the interval which you want your killing and death sprees to occur at.  See the [Killing/Death Spree Configuration Page](Configuring_Sprees.md) for more information.

Once the above two cvar's are set, you are ready to configure your killing and death sprees.

**Reference**

  * Cvar: g\_sprees, set to the name of your spree settings file. Default: "sprees.dat"
  * Cvar: g\_spreeDiv, set to the interval for Killing / Death Sprees to occur at. Default: 5.

### Multi-kills ###

Once you have the cvar "g\_sprees" set,  you can enable multikills with the cvar "g\_altExcellent".  Setting "g\_altExcellent" to 1 enables them, 0 disables them. They are disabled by default.

Note: Turning on Multi-kills disables the stock "Excellent" sound from being played on the client.  If "g\_altExcellent" is enabled and no Multi-kills are defined in the spree settings file, the server will revert to stock behavior.  Please see the [Configuring Multikills Page](MultKill_Config.md) for more information.

**Reference**

  * cvar: g\_altExcellent, set to "1" to enable, "0" to disable, Default: 0.

---


Next Page: [Configuring Killing / Death Sprees](Configuring_Sprees.md)

Previous Page: [Sprees / Multikills Home ](Sprees_and_Multikills.md)