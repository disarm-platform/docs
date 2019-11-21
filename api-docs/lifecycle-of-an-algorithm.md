# Lifecycle of an algorithm

We think about a function having 4 steps, to bring from an idea to a remotely-deployed and accessible service.

1. **Write** an algorithm which solves a problem
2. **Re-write** the algorithm so it is more robust and reliable
3. **Package** the algorithm to be accessed remotely by HTTP request and deployed simply via Docker
4. **Deploy** so it is accessible on a remote server, by HTTP request

### 1. Write

The first thing is to write some code to solve the problem. This can involve any or all of: developing a new algorithm or approach, writing code to implement an existing algorithm, gluing together existing algorithms and code, and so on. Depending on the problem and the way you're solving it, it can take a while to create something new, or can be very quick to pick an existing solution.

The initial output is usually brittle and regularly suffers from 'it-works-on-my-machine' errors. This is ok. To start with. Then we look at re-writing it.

There's no requirement to start this step in any particular way, but starting with a [templated function]() can simplify the later steps.

### 2. Re-write

We want to upgrade the original code to make it more robust and reliable. For example, if it references a local data file, we might instead place that somewhere on a remote server and write code to re-construct or retrieve it. We'll also want to include some validation of the incoming request parameters, to tell the user as early as possible they've given us invalid input.

We can add some automated _unit_ testing, for example, to make sure a function inside the code returns the expect values for a known input.

We'll also create a `test_req.json` file, which we try to ensure contains a simple but functioning example request, which we can use for `end-to-end` testing once the algorithm is deployed.

As with step 1, this step also does not _need_ to use any particular structure, but using a [templated function]() can simplify the next steps.

### 3. Package

If you started with a [templated function](), then this can be as simple as running `faas build`.

If not, you'll need to create a new [templated function]() and copy your code and related files into the new folder. Once they're copied across, you can also run `faas build`.

### 4. Deploy

You will need a running OpenFaas deployment, which you've logged-into using `faas login`.

Assuming you have a successful build from step 3, the deploy is simple to initiate: `faas up`. If this works, The command should output the URL of the

