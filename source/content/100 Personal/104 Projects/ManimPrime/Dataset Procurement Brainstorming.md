

## GitHub 

Scraping GitHub for Manim Code 

- Find the repositories from search
- Search over repositories and find relevant files
- Extract Manim Code
- Hopefully has a YouTube video linked in the repository somewhere that can be transcribed and match with manim code

Some downsides to the code first approach
 - Seems VERY hard to find the pairing narration that would come with it

Potentially could do some distillation where given code, chatgpt or chosen closed-source model gives the narration. Since Manim is lower trained resource than english, it should be a lot easier to get syntethic data this way than going from narration to code. 

### Code -> Synthetic Narration

It make a well enough narration, but the timings are off

**Current Explorations**:
1. Make it edit ONLY the timings of the manim code so that it can fit more naturally into a narration
	1. Instead of making a TTS script, captions instead are much easier to work with and require less moving parts as well

Current problems with this approach, the timings are still not synced, so making the narrations based on the length of the video render might be a better idea

Subproblems:
- Figure out how to create captions
- Match the timing with the visuals
- Figure out a way to render the two together
## YouTube

Among the Manim YouTube videos, we can mine the descriptions to get to their githubs.

Although the sample size would probably decrease pretty significantly, there would be a guaranteed narration  -> code paring