## Install from source

Follow the directions below to install Axentro from source:

1. install the [Crystal programming language](https://crystal-lang.org/reference/installation/)

2. Clone the [Axentro](https://github.com/Axentro/Axentro) repository from Github

   `git clone https://github.com/Axentro/Axentro.git`

3. Install dependencies

   `shards install`

4. Build the binaries:

   `shards build --release --no-debug`

5. Install the binaries on your path (might need to use sudo):

   ```
   mkdir -p /usr/local/bin/axentro

   cp bin/axe /usr/local/bin/axentro

   cp bin/axen /usr/local/bin/axentro

   cp bin/axem /usr/local/bin/axentro
   ```
   

6. You invoke the CLI binaries in your terminal by typing:

   `axe` - The command line blockchain client

   `axem` - The command line miner

   `axen` - The blockchain node
