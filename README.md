# AI Versus - Automated Viral Video Generator

A custom n8n automation workflow that generates cinematic "animal versus" viral videos. Pulls data from Google Sheets, uses AI to create unique matchups, generates photorealistic images, renders professional videos, and auto-publishes to Instagram, TikTok, and YouTube—all in one automated pipeline.

## Workflow Overview

This automation creates a complete end-to-end pipeline for generating viral short-form videos:

### 1. **Scene Generation** (GPT-4)
- Pulls a main character animal from Google Sheets
- Uses GPT-4 mini to generate 8 unique opponents from a specified category
- Each opponent comes from different environments/backgrounds

### 2. **Image Generation** (PIAPI with Flux1-Dev)
- **Close-up Prompts**: Generates fierce, photorealistic close-up images of both the main character and each opponent
- **Battle Aftermath**: Creates cinematic images of the winner standing over the defeated opponent
- All images are 1024x1024 or 540x960 (mobile optimized)

### 3. **Video Rendering** (Creatomate)
- Combines 8 battle scenes into a single video using a professional template
- Includes background music and dynamic text overlays
- Final output ready for social media

### 4. **Auto-Publishing** (Blotato)
- Simultaneously publishes to:
  - **Instagram** (with proper metadata)
  - **TikTok** (marked as AI-generated with public settings)
  - **YouTube** (as unlisted video)

## Required Setup

### API Keys & Accounts Needed:
1. **Google Sheets OAuth** - To read/write video data
2. **OpenRouter API** - For GPT-4 and GPT-4 mini models
3. **PIAPI** - For Flux1-Dev image generation
4. **Creatomate** - For video rendering (with template)
5. **Blotato** - For social media auto-publishing

### Configuration Steps:

1. **Google Sheet Setup**
   - Create a Google Sheet with columns: Main Character, Opponents, Status, 1.1-8.3, Final Video
   - Add animal names in the Main Character column
   - Set Status to "To Do" to trigger the automation

2. **API Configuration**
   - **OpenRouter**: Get API key from openrouter.ai for GPT-4 access
   - **PIAPI**: Create account at piapi.ai for Flux1-Dev image generation
   - **Creatomate**: Build a video template with 8 scenes for the animal battles
   - **Blotato**: Get API credentials for social media publishing

3. **Scheduling**
   - Schedule Trigger is configured to run on your preferred interval
   - Executes entire pipeline automatically

## Workflow Architecture

```
Schedule Trigger
    ↓
Get Main Character (Google Sheets)
    ↓
Scene Creator (GPT-4 mini)
    ├→ Opponents (parse 8 scenes)
    └→ Main Character (extract data)
    ↓
Merge
    ├→ Image Prompt Generator (Close-ups)
    │   └→ Generate Close Ups (PIAPI)
    │       └→ Add Close Ups to Sheet
    │
    └→ Winner Image Prompt (Battle Aftermath)
        └→ Generate Scene (PIAPI)
            └→ Add Winner Images to Sheet
    ↓
Get Elements & Render Video (Creatomate)
    ├→ Instagram
    ├→ TikTok
    └→ YouTube
```

## Performance Notes

- **Image Generation Wait Times**: 90-second delays between request and retrieval (PIAPI processing time)
- **Total Execution Time**: ~8-12 minutes per video (including processing delays)
- **Cost**: ~$2-5 per video (depending on API pricing)

## Customization

### Modify Image Styles
Edit the system prompts in:
- **Image Prompt Generator** - Adjust close-up image style
- **Winner Image Prompt** - Customize battle aftermath descriptions

### Change Social Media Settings
- **Instagram node**: Customize caption format
- **TikTok node**: Toggle AI generation flag, duet/stitch settings
- **YouTube node**: Change privacy level (unlisted/public)

### Adjust Video Template
- Replace `YOUR TEMPLATE ID` with your Creatomate template
- Modify image dimensions in PIAPI nodes (currently 1024x1024 for close-ups, 540x960 for scenes)

## Error Handling

If a video fails to generate:
1. Check API credentials in the nodes
2. Verify Google Sheet is accessible and properly formatted
3. Check PIAPI/Creatomate limits haven't been exceeded
4. Review OpenRouter API usage

## Future Improvements

- Multi-animal tournament brackets
- Custom background music upload
- Video preview before publishing
- Batch processing (multiple animals per run)
- Analytics integration to track performance
- Custom AI model selection
- Advanced prompt templating

---

## Key Features

- **Fully Automated**: Trigger once, get a complete video (8-12 minutes)
- **Multi-Platform**: Auto-publishes to 3 major social networks simultaneously
- **AI-Driven Matchups**: GPT-4 generates dynamic, realistic animal opponents
- **Professional Quality**: Photorealistic images + video editing in one pipeline
- **Cost Effective**: Automates hours of manual work for under $5 per video

## How It Works

1. Add an animal name to Google Sheets
2. Workflow pulls from sheet and triggers automation
3. AI generates 8 unique opponents for that animal
4. Creates close-up images + battle aftermath images
5. Renders a complete short-form video
6. Posts to all 3 platforms with optimized captions
7. Updates Google Sheet with final video URL

**Status**: Active | **Last Updated**: June 2026