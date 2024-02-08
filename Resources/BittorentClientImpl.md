# Bittorrent Client Implementation

## Source: [Creating a Bittorrent Client using Asyncio](https://www.youtube.com/watch?v=Pe3b9bdRtiE)

- Uses and Users:

    - Gaming Companies; blizzard, eve, etc.
    - Education
    - Government
    - Entertainment
        - Including pirating
    - Tech companies
        - Facebook, Twitter

### How does torrenting work?

- Torrent File --> Torrent Client Parses the file and find the tracker --> Get the list of peers from where we can download the piece of file.

### Why Asyncio?

- Maintain multiple concurrent connection to peers
- Network I/O bound application - waiting for data

- Single process, single threaded approach for concurrent applications
- Application code yields control at optimanl times

### Asyncio Building Blocks

- 

