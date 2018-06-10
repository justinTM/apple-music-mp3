# Apple Music MP3

Automatically swap mp3 versions of Apple Music songs in your library. 

This is needed for compatibility with Traktor DJ software which can't play DRM-locked proprietary files like .m4a used by the Apple Music streaming service.

## Process flow
1) ### New song added
    When a new song is added to a user’s library from Apple Music, we’ll need to trigger the process to start. Depending on the Apple Music API, we may or may not be able to know immediately when this happens. If there’s no way to get a “push notification” when a song’s added, we might need do a search of the library (periodically, or at the user’s request) to find new songs.

2) ### Get the song metadata
    From the API, we’re able to get information like artist, song title, album artwork URL, lyrics, etc.
We’ll scrape all of this metadata from the Apple Music song, and later apply it to the mp3 version. 

3) ### Find the song online
    We’ll try to find the song online where we can download it for free. This will involve doing a search of the artist+title. There’s a Google API we could use to leverage their algorithm, or we could just try to “dumb search” by finding titles like “artist - song title”. The two most likely sources will be SoundCloud and Youtube. There are cmd downloaders like youtube-dl and scdl we could utilize.

4) ### Verify we got a match
    This might be too hard and therefore unnecessary, but it would be a good idea to confirm the mp3 is the same song as the apple music version. Could be a manual user check (eg. the user listens to each one and says “yep that’s right”) or maybe a fingerprint analysis of the two files and a confidence rating of the match.

5) ### Combine metadata
    This is easy! Strings are a direct swap (artist, title, etc.). We’ll grab the artwork URL of the original, download it, apply that to the replacement. Get lyrics of the original and find a way to store those in the mp3.

6) ### Replace original with mp3
    We’ll need to use the Apple Music API to remove the original and add the mp3 in-place. This requires knowing where the original is located (ie. which playlist(s) the song is added to).



