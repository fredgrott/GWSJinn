GWSJinn
=======

Set of build scripts using Lombok, RxJava, Dagger2, ect.

Implementation
==============

The idea is to combine supplying the tools, libs, etc with setting up a developers work-flow that
empowers the android developer and the team that android developer communicates with.

Beginning with the top, I split out my dependencies and continuous-integration server set-up to separate
gradle files at the root folder buildsystem and the code QA settings will be done the same way as it
makes the resulting root build.gradle and module build gradle file easy to understand and read.

If I need to apply a gradle plugin to the app module in different environments, for example genymotion plugin gets
applied to app module on non-ci environment, than its also done as a gradle file snippet in this root folder.

Some choose to abstract the layers of the application as a set of gradle project modules, I choose instead
to implement that as names in packages instead due to the number of product flavors I am using to make it
easier to track on application projects.

Thus, given that with using dagger I have to have some gradle product Flavors already I add some to allow
the implementation of:

    -Mocking of instrumented testing(its a Google recommendations, ie best practices)
    -A flavor that allows me to do design overlays, while debug does allow me to combine scalpel, madge,
     and probe into a view type debug toolbar I still need to get feedback from non-programming designers
     on the team and this flaovr helps do that.
    -A sharedTest folder to share certain junit code between androidTest, androidTestMock, and test
    -The release flaovr is labeled prod

I use several gradle product flavors to assist me in enabling certain debug tools that are specific for
data debugging, view and layout debugging, and design feedback with design staff. The code used is soft forks of
other 3rd party efforts but they did not see the advantage of being able to turn it off and on via their
implementation so one could enable it on a per gradle product flavor basis, they lacked vision!

The set of gradle plugins helps me with the gradle work-flow and the android  development work-flow
I have to implement, namely:

    -Godot plugin allows me to fine-tune the gradle builds as far as performance
    -Hugo plugin allows me to implement annotation-triggered method call logging in my debug builds
    -Spoon-Gradle plugin allows me to use the spoon library to run and collect instrumented tests on
     every device and emulator
    -Apt plugin is needed for the new version of butterknife(version 8) and for dagger2 as it sets things
     properly as far as the annotation processors
    -AdvanceBuildVersioning plugin allows me to set policies on versioning both the app moduel and
     library module artifacts automatically.
    -AndroidMavenTasks plugin allows me to generate library module maven artifacts to allow me to
     either upload to jcenter or deploy to jitpack
    -Probe plugin allows me intercept view methods and thus alloows me to debug views and layouts
    -Frodo plugin allows me to debug rxJava in that it allwos me to annotation trigger logging of Observables
     and Subscribers

Okay, so now I detail the specific android libraries I am using that pertain to the android development
work-flow:

    -SpoonClient lib enables rest of spoon-gradle as far as getting screenshots automatically gnereated
     for each device and emulator that executed tests
    -GwsDroidInsUtil lib provides the rest of the turn off system animations during testing solution
    -DBInspector lib allows me to look at the database files without needing to root a device
    -LeakCanary allows me to diagnos memory leaks
    -Timber allows me to keep debug logging staying in debug builds only
    -GWSDroidViewServer allows me to use the android sdk Hierarchy tool to debug and inspect
     the view groups and layout stuff
    -GWSWakeUp library used to wake up devices when I push apps to test them
    -Scalpel to assist in debugging layout layers, etc
    -Madge library to debug of whether assets are drawing at their native resolutions


And of course, to set-up an android application properly so that I get to coding the business logic and
implementing the UI I need to use some specific libraries that set-up some boilerplate code covering everything
from computing a proper Application User Universal ID for app tracking and app reports to bolireplate
code to display a customized Eula for users.