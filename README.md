# AAE_021_CoaxialDrone
[Vehicle dynamics](https://en.wikipedia.org/wiki/Vehicle_dynamics) are concerned with the motion of bodies under the action of forces. For our purposes, vehicle dynamics references understanding how the rotatation of the quadrotor's four rotorss create forces and how these forces generate motion of the vehicle.

Over the next few notebooks, we'll learn how to model these motions, mathematically, in Python.

To understand the dynamics/motion of a quadrotor, we need to understand the forces that act upon the quadrotor. Namely, thrust, gravity, and drag.

For the following notebooks, we'll focus on the thrust generated by the quadrotor's rotors and the downward force of gravity (mass). In practice, we usually treat drag as a disturbance when designing quadrotor controllers and don't model it explicitly; as, the the effects are relatively small at lower vehicle and wind speeds and it's difficult to identify the correct drag model.

![thrustforce](images/thrust_force.png)

Force is a vector; thus, when analysing force, we must know the size/magnitude of the vector, as well as the direction.

For gravity, the vector always points downward, toward the center of the Earth. The strength of the force is given by m * g where m is the mass of the quadrotor and g is the acceleration due to gravity (approximately 9.81 m/s^2).

The strength of the thrust vector depends on the size and shape of the rotor's blades and on how fast they are spinning. The direction of thrust is always perpendicular to the plane within which the rotor is spinning.

In order to stay airborne, the quadrotor must exert a force, with its rotors, at least equal that of the downward force of gravity -- creating a hover (translational equilibrium). (As with all forces, the size of these forces are measured in [Newtons](https://en.wikipedia.org/wiki/Newton_(unit))).

For the moment, let us consider a monorotor vehicle. If given a monorotor with a downward, gravitational force of 100 Newtons, what can be said about the value of F_thrust in order to keep the vehicle in a hover? F_thrust must, also, be 100 Newtons. What would be an expression for the mass of this vehicle? m = 100/9.81. (About 10.2 kg)

Even though hovering in a state of translational equilibrium, the monorotor cannot be in a state of rotational equilibrium. In addition to causing a thrust force, a rotating rotor also introduces what is called a moment or torque. A rotor that is rotating clockwise (CW) will produce a moment that causes the body to rotate counter-clockwise (CCW).

As is the case with helicopters and multirotors, a second rotor is introduced in order to cancel out this rotational force. (In the case of a helicopter, it is most often the tail rotor.) In looking at multicopters, you'll notice most to be designed with an even number of rotors (quad, hex, octo, etc). Each rotor spinning CW has its compliment rotor spinning CCW to negate rotation force (most often adjacent from one another).

The rotors that rotate CW introduce a CCW moment and the rotors that rotate CCW introduce a CW moment. If the CW rotors are spinning faster than the CCW rotors, then the CCW moments produced by those rotors will dominate and the vehicle will yaw in the CCW direction. But, at what rate will it yaw; what are the magnitudes of the moments and forces that the rotating rotors produce?

![rotorphyics](images/rotor_physics.png)

We use the lowercase, greek letter omega(ω) to represent the rotation rate of a motor and this rate is measured in units of rad/s. (So, when ω = π, the rotor is completing one rotation/second.)

It turns out that, when a rotor is rotating with a rotational rate omega, the thrust produced and the induced moment are both proportional to omega^2. The constant of proportionality we call K sub f for force and K sub m for moment. The actual value of these constants depend on the size and shape of the blades, the specific motors used, as well as the density of the surrounding air that they operate in. (In practice, we usually obtain these values empirically.)

![fvo](images/force_vs_omega.png)

Based on the Force vs omega graph shown above, what is k_sub_f for this propeller? 0.007. If you double the rotation speed of the rotor, how does the thrust change? It increases by a factor of 4.

