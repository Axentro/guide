## Install from source

Follow the directions below to install SushiChain from source:

1. install the [Crystal programming language](https://crystal-lang.org/reference/installation/)

2. Clone the [SushiChain](https://github.com/SushiChain/SushiChain) repository from Github

   `git clone https://github.com/SushiChain/SushiChain.git`

3. Install dependencies

   `shards install`

4. Build the binaries:

   `shards build --release --no-debug`

5. Install the binaries on your path (might need to use sudo):

   `mkdir -p /usr/local/bin/sushichain

   cp bin/sushi /usr/local/bin/sushichain

   cp bin/sushid /usr/local/bin/sushichain

   cp bin/sushim /usr/local/bin/sushichain

   `

6. You invoke the CLI binaries in your terminal by typing:

   `sushi` - The command line blockchain client

   `sushim` - The command line miner

   `sushid` - The blockchain node