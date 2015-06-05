[![Build Status](https://travis-ci.org/sippy/voiptests.svg?branch=master)](https://travis-ci.org/sippy/voiptests)

# VoIP Intergated Tests Suite

This is a "meta-repository" to test interoperability of several popular
open-source VoIP components and their ability to handle basic SIP call
scenarios, both individually and working as a simple VoIP switching system.

The basic test setup looks like the following:

![Alt text](https://docs.google.com/drawings/d/1vGkoxKZxv-acAAs5azTOApArSMWqBz9vIN83TXyIZAM/pub?w=960&h=720 "Test Setup")

In the course of the test, first UA, which we call "Alice", initiates number
of distinct SIP sessions to SSuT, which is then expected to forward those
sessions to the second UA ("Bob"). The Bob either answers or rejects
the specific session (depending on session number passed in the user section
of the RURI) and Alice verifies that the particular session has completed
in expected way.

Both Alice and Bob also check that the SSuT rewrites the SDP correctly,
replacing original random media IP/port with the IP/port of the RTPProxy,
which signifies proper execution of the RTPProxy Control Protocol (RTPPC)
between the particular SSuT and the RTPProxy.

Also, upon test completion some basic statistics is pulled from the RTPProxy
to verify that the number of RTPPC requests/replies matches pre-determined
value specific for that SSuT and that there were no errors detected in the
protocol exchange.
