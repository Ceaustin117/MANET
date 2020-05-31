# MANET
Fig 6 is improved by using an algorithm so that the nodes can find each other in a situation 
where they have been unable to detect other devices. In the event they are able to detect other devices they are more likely to be on the same channel and establish a connection quicker. Which is very important in military or other time critical situations. This method is especially useful 802.11n wireless network communication channels which can have 24 channels. Future implementations might have even more. Improved results compared to purely random are shown in the link below. Followed by the random and new random_remainder algorithm written in python3.

<p align="center">
  <img src="https://github.com/Ceaustin117/MANET/blob/master/improvements.png" width="350" title="hover text">
</p>



Random Method

       def set_random_channel(self):
                random_number = random.randint(1, self.number_of_channels)
                return random_number

Improved Method using a combination of randomization and remainder math.

        def random_remainder(self):
                flag_primary = False
                flag_secondary = False
                number_of_channels = self.number_of_channels
                remainder = number_of_channels + 1
                while not flag_primary:
                    if self.primary_radio == number_of_channels:
                        self.primary_radio = random.randint(1, number_of_channels)
                    elif self.primary_radio == 0:
                        self.primary_radio = random.randint(1, number_of_channels)
                    else:
                        self.primary_radio = (self.primary_radio * random.randint(1, number_of_channels)) % remainder
                    if self.primary_radio != 0:
                        flag_primary = True
                while not flag_secondary:
                    if self.secondary_radio == 0:
                        self.secondary_radio = random.randint(1, number_of_channels)
                    elif self.secondary_radio == number_of_channels:
                        self.secondary_radio = random.randint(1, number_of_channels)
                    else:
                        self.secondary_radio = (self.secondary_radio * random.randint(1, number_of_channels)) % remainder
                    if self.secondary_radio != 0:
                        flag_secondary = True
