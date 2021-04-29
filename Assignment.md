# Introduction
Today we will look at a complex system that many of you will be very familiar with: the Dutch rail schedule. Optimal scheduling in large complex networks (such as our rail system) is notoriously hard. Networks like this have to be balanced between efficiency and robustness. We want our system to be as fast as possible, while also functioning when things go wrong.

This folder contains two csv files: one with the stations and their coordinates, the other with all connections and their respective durations. First, construct a visualization of the rail network with the stations as nodes and the right connections between them.

Example of a visualization of the railway network from the NS.
![Example Visualization](https://github.com/ardanwan/CLS-Hackathon/blob/74c17b86214da976704d8fc30e0f6746ae9eb2c9/Complex%20Systems/Example%20Rail%20Visualization.png)

# Assignment
In this assignment we are interested in two things: efficiency and robustness of our schedules. First you will attempt to find the most optimal schedule you can find. A schedule consists of up to 5 different trajectories, with a maximum duration of 3h per trajectory. Each station can only be visited once in each trajectory. The efficiency of the schedule is determined by a score function:

- S = ρ * 10000 - (20N<sub>t</sub> + t / 10)

In the file containing all stations, some are marked as 'critical'. These are important traffic hubs, which are vital for distributing the flow of passengers. The variable ρ in the score function is the fraction of critical stations that is serviced by at least 1 trajectory. N<sub>t</sub> is the total number of trajectories and t is the total service duration of all trajectories in minutes. We demonstrate the scoring system with an example schedule:

The example schedule consists of 3 trajectories:
- Den Haag Centraal - Leiden Centraal - Schiphol - Amsterdam Sloterdijk - Amsterdam Centraal - Almere - Lelystad | total 89 minutes
- Groningen - Assen - Zwolle - Amersfoort - Utrecht Centraal - s'Hertogenbosch - Eindhoven - Weert | total 168 minutes
- Den Helder - Alkmaar - Hoorn - Zaandam - Beverwijk - Haarlem - Sloterdijk - Amsterdam Centraal - Amsterdam Amstel - Hilversum | total 180 minutes

This schedule services 11 out of 23 critical stations, so ρ = 0.4783. This schedule would receive a score of S = 4783 - (60 + 44) = 4679. Of course you will find much better scoring schedules. Be warned however, finding the optimal solution (or even a good solution) is not trivial at all!

Besides finding an optimal score for our rail schedule, we also want to know how robust our schedule is. Rail trouble happens almost every day and a good schedule should take it into account. To simulate our railway trouble, we randomly take away two connections in any of the trajectories of your schedule (can be from different trajectories). Some trajectories should now be split (or shortened if it was a final destination). To deal with this, you may reconnect all separated stations via another route, if possible. If multiple trajectories use a compromised connection, they all have to be rerouted (or cancelled). Rerouting will disgruntle passengers because of delays, while completely cutting connections can leave people stranded. We measure our schedule robustness through a penalty function:
- P = 2t<sub>additional</sub> + 500N<sub>not-rerouted</sub>

Here t<sub>additional</sub> is the additional time in minutes of the rerouted connections and N<sub>not-rerouted</sub> is the number of stations that cannot be rerouted at all. If multiple trajectories are rerouted on the same connection, they all contribute to the additional time. To compare different schedules, we cannot simply compare their penalty scores with random connections. To get a sense of the robustness we calculate the average penalty of two random connections cut and compare these scores.

That's all the instructions! Build your rail network and look for your most efficient and most robust networks. Try to make a top three of both and visualize them all. Visualize what happens when the two random connections drop out and the trains are rerouted. Are your most efficient schedules similar if you visualize them well? What about your most robust networks? And how do your efficient networks score in robustness and vice versa?

For more reading on [networks in complex sytems](http://networksciencebook.com/chapter/2) and [network robustness](http://networksciencebook.com/chapter/8#introduction8) (Not needed for the assignment)
