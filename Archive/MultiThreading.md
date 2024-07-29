<< [README](README.md)

# Multi-threading

## Contents
- [Overview](#overview)
- [Thread States](#thread-states)
- [Runnable Interface](#runnable-interface)

## Overview
- Splits different tasks across different threads to be done concurrently
- By default, Java apps run Main on one thread
- Performance is increased when using multithreading, at the cost of more power usage

## THREAD STATES
- NEW -- Created but not yet started
- RUNNABLE -- Thread has started
- BLOCKED -- Thread is waiting on some lock before continuing
- WAITING -- Thread is waiting indefinitely
- TIMED-WAITING -- Thread is waiting for a specified amount of time
- TERMINATED -- Thread is finished

## RUNNABLE INTERFACE
- Defines a task to be run by a thread
- Contains a single run() method, holding the code to be executed
- Allows for multiple interfaces to be implemented, and for a class to be extended
- Separates the task logic from thread management