# chemical_pronter

This repo contains CAD files (and soon assembly instructions) for a modular fluid routing system designed for chemical printers. It is readily and inexpensively manufacturable at home with a 3D printer and inexpensive off the shelf materials.

## The design premise

In ye olden days of yore, chemists didn't have any of that fancy ground glass stuff that's so popular in chemistry labs today. They had stoppers and tubes, and by golly it worked. When you needed to connect a flask up to a distillation column, you shoved a stopper with a hole in it into the top of the flask, put in a little stubby bit of flint glass tubing while trying not to stab yourself, and then stuck some silicone tubing (or latex, if you were a poor) on to that. You then shoved the other side of the squishy tube onto your condenser, which had hose barb fittings because back in cave man times that's all we had.

If you needed a reflux column instead, you connected the tube to the other end of the condenser, and bob's your uncle.

You could actually assemble a lot of fun and handy apparatus with nothing but basic flasks and rubber tubing. It may not have been as elegant as 24/40 ground glass fittings, but the only part you really needed ground glass on was your sep funnel, which is why sep funnels cost roughly a bajillion dollars back then. Anyway, the point is, it worked, and was doable with garage equipment.

This system is very loosely inspired by that approach. But instead of plugging up tubing and stoppers with our primitive sausage-fingers, this system does it all with valves. One specific type of valve in particular. But we'll get to that in a second.

## The abstraction

Most "things" that you will encounter in a chemistry lab can be accurately represented with the following ludicrously oversimplified model:

fluid input--->[device]---->fluid output

For example, let's take the condenser. If we ignore the water circulating through the jacket, a fluid (in the proper sense - liquid or gas) goes in one end and out the other.

If you want to reflux something, you would attach the bottom of the condenser to a boiling flask, and leave the top open. The flow would thus be something like this:

Boiling flask ---> condenser bottom ---> condenser top ---> open air

But what if you want distillation? Well, we need a second flask, but that's about it. That flow would look something like:

Boiling flask ---> condenser top ---> condenser bottom ---> receiving flask ---> [open air, or vacuum if you're fancy like that]

So all we need to move between these two setups is to change which end of the condenser goes to the boiling flask, really, and if we're feeling ambitious to skip the recieving flask.

This abstraction generalizes well. Most lab apparatus can be assembled with each "device" being considered as some arbitrary thing with a fluid input and a fluid output, and tubes in the right places to hook all the right inputs to all the right outputs.

So, that's what the valve does.

## The valve

If you're a valve nerd, this is technically a 3-position 4-way valve. On the "input" side, you have three ports: device port A, device port B, and main loop in. These ports are just holes drilled in a round disk around a central axis, like a triforce or something, but with round holes instead of triangles. This is because drill bits for drilling triangular holes are really expensive.

So tubes go into one side of this plate, and on the other side of the plate is another round plate, also with three holes. The second plate rotates, allowing the three holes on the stationary plate to line up with the three holes on the mobile plate in any one of 3 positions. 

On the mobile plate, there is one port - main loop out - and the other two holes are just connected with a short piece of tubing.

What this allows you to do is put a device in any one of three positions:

### Bypass

If main loop in is lined up with main loop out, then the device is skipped entirely. The device's port A and port B are attached to each other, if you care about that sort of thing, which you probably don't.

### Forward

If the mobile plate is rotated 120 degrees clockwise, things start to get interesting. Now, the path is:

main loop in ---> short loopback tube ---> device port A ---> [device] ---> device port B ---> main loop out

We've effectively diverted the flow, and added our device to the main path!

### Reverse

If the mobile plate is rotated 120 degrees *counterclockwise*, then things get even more interesting. Now the path is:

main loop in ---> device port B ---> [device] ---> device port A ---> short loopback tube ---> main loop out

Simply by changing the valve position, we have "flipped our condenser upside down" so to speak. If our device is a condenser, that is. But anyway, we're still diverting the main flow through our device, but now it's going through our device in the other direction.

## The implication

This means that you can take all your equipment - your pumps, your reactor, your condensers, a bunch of old mason jars filled with solvents and reagents, your filtration setup, whatever - throw it all in one big main loop, and then let the software figure out how to hook it all together to make whatver setup you need. It effectively reduces apparatus assembly into a software pathfinding challenge, and any software guy can tell you, if there's a way, A* will find it.

But most importantly, you can serialize operations. With just software. A 10-step synthesis can be performed by literally just putting the right starting materials in the right jars, hitting "print", and walking away.

Actually no, please don't walk away, it probably is a good idea to keep an eye on it with a fire extinguisher, just in case. But you get the idea.

Also, side note, a loop can be a device too, allowing for subloops. This probably has some implications or something, if I knew topology better maybe I could tell you what they were. 

## ToDo: Finish the rest of the docs

