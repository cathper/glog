CloudFormation, a love-hate relationship
=========================================

I love to provision stuff with just a JSON file and some parameters. It's really
an ERB file where cloud init scripts are put into the UserData. Anyway, it's
great. However, when I meet the limitations I hate it.

Here are some of the limitations that makes me hate CloudFormation:

#.  You cannot create a VPN connection with static routing.

#.  You cannot attach multiple EIPs to an ENI because you cannot assign multiple
    private IPs to an ENI.

And when you meet those limitations you cannot do anything else but create
another CloudFormation stack that does the rest; and launching the entire
environment is a process where you create a stack, do something manually (or in
a script---which is what you try to avoid using CloudFormation), create another
stack, do something manually etc.

I would *love* to have a complete description of my environment in a plain text
file that can be version controlled. The wet dream: a version controlled
environment.

"Use RightScale, you 'tard." No. How should that be any better when they
obviously become more and more multi-cloud and I really just care about AWS for
now? They must be going in another direction that I will prefer.

Somebody should make a cloud-agnostic version of CloudFormation that supports
everything. I'm not sure CloudFormation is the best way to do that. It should be
declarative, easily parseable, maintain the environment over time.

