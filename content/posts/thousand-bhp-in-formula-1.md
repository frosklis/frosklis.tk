---
draft: false
layout: post
title: Thousand BHP in Formula 1?
categories: Random calculations
tags: [formula 1]
date: 2015-03-27
---

With the new <a href="https://www.fia.com/file/13068/download?token=dkh9nZET">regulation of Formula 1</a>, an emphasis has been put in cost reduction and hybrid technology development. I think it is far too regulated and do not really believe that a cost reduction has been achieved (though I do no have data to back it up). Anyway, thousand horsepower?

That is a psychological barrier and honestly, difficult to answer. Right now, F1 cars do not have engines, they have "power units". The power unit has a traditional 6-cylinder atmospheric combustion engine, a battery, and an electrical engine.

Anyway, let's make some numbers.

Petrol has around 45,000 kJ/kg. Say F1 cars can get special petrol, so 50,000 kJ/kg. With the current regulations, fuel flow is limited to 100 kg/h (article 5.1.4). That yields 5,000,000 kJ/h. A Watt is one Joule per second and one horse power is 735 Watts.

So 5,000,000 / 3600 = 1388 kW.

BUT. That is thermal power, the amount of mechanical power that can be extracted from thermal power is limited by <a href="https://en.wikipedia.org/wiki/Carnot_cycle">Carnot's theorem</a>. For power plants that produce electricity that is around 35%. For a car it doesn't even reach 20%.

1388 x 0.2 = 278 kW = 378 horse power.

That gives only <em>378 horse power</em> for the combustion engine in the power unit. I have been generous with the numbers.

Now the electrical part. Electrical energy can be converted to mechanical energy with almost no loss, so I will assume 100% efficiency. According to regulations (article 5.2.3), the torque is limited to 200 Nm and the revolutions to 50,000 rpm.

200 Nm x 50,000 rpm = 167 kW

167 kW from the electrical part + 278 kW from the combustion part = 445 kW = approx 600 horsepower, very far from both 1,000 horsepower.

One answer and one question:

* No, I do not see thousand horse power happening, unless the maximum flow rate is increased.
* 2015 F1 cars are reported to have around 850 horse power. Where do they come from? Someone please explain.
