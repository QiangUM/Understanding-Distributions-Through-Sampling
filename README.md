# Understanding-Distributions-Through-Sampling
This is Cousera Applied plot practice assigment


import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import matplotlib.animation as animation

%matplotlib notebook

# generate 4 random variables from the random, gamma, exponential, and uniform distributions
x1 = np.random.normal(-2.5, 1, 10000)

x2 = np.random.gamma(2, 1.5, 10000)
x3 = np.random.exponential(2, 10000)+7
x4 = np.random.uniform(14,20, 10000)


# plot the histograms
plt.figure(figsize=(9,3))
plt.hist(x1, density=True, bins=20, alpha=0.5)
plt.hist(x2, density=True, bins=20, alpha=0.5)
plt.hist(x3, density=True, bins=20, alpha=0.5)
plt.hist(x4, density=True, bins=20, alpha=0.5);
plt.axis([-7,21,0,0.6])

plt.text(x1.mean()-1.5, 0.5, 'x1\nNormal')
plt.text(x2.mean()-1.5, 0.5, 'x2\nGamma')
plt.text(x3.mean()-1.5, 0.5, 'x3\nExponential')
plt.text(x4.mean()-1.5, 0.5, 'x4\nUniform')




x = [x1, x2, x3, x4]

# use plt.subplots 4 ax
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, sharey = True)

ax = [ax1, ax2, ax3, ax4]

#set  xlim and ylim of each ax
axis1 = [-7.5, 2.5, 0, 0.6]
axis2 = [-0.5, 10, 0, 0.6]
axis3 = [2, 17, 0, 0.6]
axis4 = [12, 22, 0, 0.6]
axis = [axis1, axis2, axis3, axis4]

#set the bins for every ax
bins1 = np.arange(-7.5, 2.5,0.2)
bins2 =np.arange(0, 10,0.2)
bins3 = np.arange(7, 17,0.2)
bins4= np.arange(12, 22,0.2)
bins =[bins1,bins2,bins3,bins4]

#set the ax's title
titles = ['x1 Normal', 'x2 Gamma', 'x3 Exponential', 'Frequency']

#define  update function 

def update_subplot(curr):
    if curr == 100:
        a.event_source.stop()
    for i in range(0,len(ax)):
        ax[i].cla()
        ax[i].hist(x[i][:100*curr], normed = True, bins = bins[i])
        ax[i].axis(axis[i])
        ax[i].set_title(titles[i])
        ax[i].set_ylabel('Frequency')
        ax[i].set_xlabel('Value')
    plt.tight_layout()
        

a = animation.FuncAnimation(fig, update_subplot, interval = 100, repeat = True)
