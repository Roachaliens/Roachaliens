![starryai-0-146034770-1-0-photo (1)](https://user-images.githubusercontent.com/130972957/236614546-0d869dc8-6924-4974-bcde-9d9d0c210562.png)
- 👋 Hi, I’m @Roachaliens
import hashlib

import datetime as date

class Block:

    def __init__(self, index, timestamp, data, previous_hash):

        self.index = index

        self.timestamp = timestamp

        self.data = data

        self.previous_hash = previous_hash

        self.nonce = 0

        self.hash = self.calculate_hash()

    def calculate_hash(self):

        hash_data = str(self.index) + str(self.timestamp) + str(self.data) + str(self.previous_hash) + str(self.nonce)

        sha = hashlib.sha256()

        sha.update(hash_data.encode('utf-8'))

        return sha.hexdigest()

class Blockchain:

    def __init__(self):

        self.chain = [self.create_genesis_block()]

        self.difficulty = 4 # Number of leading zeros required for a valid hash

        self.reward = 100000 # Satoshis added for each new block

    def create_genesis_block(self):

        return Block(0, date.datetime.now(), "Genesis Block", "0")

    def get_latest_block(self):

        return self.chain[-1]

    def add_block(self, new_block):

        new_block.previous_hash = self.get_latest_block().hash

        new_block.timestamp = date.datetime.now()

        new_block.hash = new_block.calculate_hash()

        self.chain.append(new_block)

    def mine_block(self, miner_address):

        reward_transaction = Transaction("0", miner_address, self.reward)

        transactions = [reward_transaction]

        previous_block = self.get_latest_block()

        new_block = Block(previous_block.index + 1, date.datetime.now(), transactions, previous_block.hash)

        while not self.is_valid_hash(new_block.hash):

            new_block.nonce += 1

            new_block.hash = new_block.calculate_hash()

        self.add_block(new_block)

        return new_block

    def is_valid_chain(self):

        for i in range(1, len(self.chain)):

            current_block = self.chain[i]

            previous_block = self.chain[i-1]

            if current_block.hash != current_block.calculate_hash():

                return False

       
-

<!---
Roachaliens/Roachaliens is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
---> jeraldroach3333@gmail.com 
