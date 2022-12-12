+++
title = "What is 12-factor app design"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2022-11-11T05:00:00Z
description = "12 factor app"
categories = ["network"]
type = "post"

+++
Apps that follow the 12-factor app design process benefit from inherent cloud nativity. Sounds interesting? Let’s take a look at the process.

12-factor app design is a methodology for designing cloud native apps – almost like a pattern that you can follow. You can use this super-flexible process with any programming language and any combination of backing services. 

In addition to being cloud native, apps that use the 12-factor methodology deliver maximum portability and can scale up without the need for any significant changes. Their automated setup makes it easier and faster for new developers to come on board, while divergence between development and production is minimised, resulting in maximum agility.

Intrigued? Then let’s review each of the 12 factors in more detail.

1. Codebase

A 12-factor app has a single codebase. This is a code repository or a set of code repositories that share the same root commit. There can (and will) be multiple deploys of the app, but never more than one codebase.

2. Dependencies

12-factor apps use a dependency declaration manifest to declare all dependencies, without relying on the existence of system-wide packages. A dependency isolation tool is used during execution to ensure this is maintained, with the explicit dependency specification applied evenly across production and development.

3. Config

If you’re creating a 12-factor app, you need to separate config (all those parts such as staging, production and developer environments that vary between deploys) from the app’s code. This means that the code remains the same across all deploys, despite variations in the code.

4. Backing services

 Apps consume backing services such as datastores, caching systems and messaging systems as part of their regular operation. 12-factor apps make no distinction in their code between such locally managed systems and those managed by third parties, such as binary asset services and metrics-gathering services, treating both as attached resources.

5. Build, release, run

 The 12-factor app incorporates clear divisions between the build, release and run stages of its development. These three stages transform the codebase into a deploy. Once one stage of this process is complete and the next is underway, it is not possible to go back and change the code in the previous stage.

6. Processes

12-factor apps are executed as stateless processes. These processes share nothing, with any persistent data stored via a backing service such as a database. The app doesn’t rely on anything being cached in memory or on disk.

7. Port binding

 A key element of creating a 12-factor app, port biding means the web app can export HTTP as a service and listen to incoming requests without being executed inside a webserver container. Instead, it is entirely self-contained, creating a web-facing service without relying on a webserver for runtime injection. 

8. Concurrency

In the 12-factor app, types of work are assigned to different process types. The processes are executed in a similar way to the Unix process model, with concurrency meaning that the tasks can be executed out of order and the result is no different than if they had been executed in order.

9. Disposability

 You can start a 12-factor app’s processes at a moment’s notice and stop them just as quickly. This process disposability delivers greater agility, meaning you can rapidly deploy code or config changes. It also allows for robust production deploys and fast elastic scaling.

10. Dev/prod parity

 A 12-factor app reduces the gaps that exist between development and production of a traditional app, thus promoting continual deployment. Developers are closely involved not just in writing code but in deploying it and reviewing the app’s resulting behaviour. Their code can be deployed within hours of writing – sometimes even minutes.

11. Logs

 Logs – the output streams for running apps, which provide visibility of their behaviour – are usually written to log-files. This is not the case with 12-factor apps. Rather, each process that runs produces an unbuffered event log in stdout. Developers can view these streams in order to understand the app’s behaviour.

12. Admin processes

With a 12-factor app, admin and management tasks are run as one-off processes, with the app strongly favouring languages that make it easy to run one-off scripts by providing an REPL shell. These one-off processes utilise the same dependency isolation techniques as the app’s regular processes.

Conclusion

Apps that follow this outline deliver outstanding agility and flexibility. They allow for new developers to get up to speed rapidly and for changes to be pushed out quickly and easily. They are also eminently scalable, with cloud nativity making them ideal for businesses with ambitious plans for future expansion. 