# KOReader Dictionary Sync Plugin

A KOReader plugin that allows you to quickly save words to your Supabase dictionary database. The plugin integrates with KOReader's built-in translation and dictionary features to automatically detect languages and translate words.

## Features

- **Automatic Language Detection**: Automatically detects source language from the document
- **Quick Save**: Save words with minimal interaction - just select a word and confirm
- **Manual Edit**: Option to manually adjust languages, translation, and add definitions
- **Supabase Integration**: Directly saves to your Supabase database
- **Auto-set Metadata**: Automatically sets status="New" and source="koreader"

## Setup

### 1. Install the Plugin

1. Copy the `dictionary-sync.koplugin` folder to your KOReader plugins directory:
   - On Android: `/sdcard/koreader/plugins/`
   - On Linux: `~/.config/koreader/plugins/`
   - On other devices: Check KOReader documentation for plugin directory location

2. Restart KOReader - the plugin should appear in the plugin management

### 2. Configure Supabase Credentials

You have two options:

#### Option A: Use .env File (Recommended - Easier on Kindle)

1. Copy `.env.example` to `.env` in the plugin folder:
   ```
   dictionary-sync.koplugin/.env
   ```

2. Edit `.env` and add your credentials:
   ```
   SUPABASE_URL=https://your-project.supabase.co
   SUPABASE_KEY=your-anon-public-key-here
   ```

3. Restart KOReader - the plugin will automatically load credentials from `.env`

#### Option B: Manual Configuration

1. Open KOReader
2. Go to **Menu** → **Dictionary Sync** → **Configure**
3. Enter your Supabase credentials:
   - **Supabase URL**: Your Supabase project URL (e.g., `https://xxxxx.supabase.co`)
   - **Supabase API Key**: Your Supabase anon/public key
4. Click **Test Connection** to verify
5. Settings are automatically saved

**Note**: If you use `.env` file, those values take priority. Manual configuration will override `.env` values if you save them.

### 3. How to Get Supabase Credentials

1. Go to [https://supabase.com](https://supabase.com) and log in
2. Select your project (or create a new one)
3. Go to **Settings** → **API**
4. Copy the **Project URL** and **anon/public key**

## Usage

### Quick Save from Word Selection

1. While reading, select a word by long-pressing or using KOReader's word selection
2. In the popup menu, tap **"Save to Dictionary"**
3. A dialog will appear - enter the translation and adjust languages if needed
4. Click **Save** to save the word
5. The word will be saved with:
   - `status` = "New"
   - `source` = "koreader"

### Manual Save from Menu

1. Select a word in the book
2. Go to **Menu** → **Dictionary Sync** → **Save Selected Word**
3. Enter word details and save

## Data Structure

Words are saved to Supabase with the following structure:

- `language1`: Source language (e.g., "English", "German")
- `word1`: The selected word
- `language2`: Target/translation language
- `word2`: The translation
- `status`: Always set to "New"
- `source`: Always set to "koreader"
- `definition`: Optional, can be added manually
- `definition2`: Optional
- `favorite`: Defaults to false

## Troubleshooting

### Plugin Not Appearing in Menu

- Ensure the plugin is enabled in Plugin Management
- Restart KOReader after installation
- Check that files are in the correct `.koplugin` directory

### Cannot Connect to Supabase

- Verify your Supabase URL and API key are correct
- Check your internet connection
- Ensure your Supabase project is active
- Check that Row Level Security (RLS) policies allow your API key to insert data

### Word Not Saving

- Check for duplicate words (same word1/word2 pair already exists)
- Verify all required fields (language1, word1, language2, word2) are present
- Check that you have internet connection
- Verify Supabase credentials are configured

## Requirements

- KOReader with plugin support
- Supabase account and project
- Internet connection for saving words
