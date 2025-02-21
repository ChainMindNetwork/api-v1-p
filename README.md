# CMD API

A Node.js API server that integrates with Supabase for agent data management.

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Supabase account and project

## Setup

1. Clone the repository
2. Install dependencies:

   ```bash
   npm install
   ```

3. Copy the environment variables template:

   ```bash
   cp .env.example .env
   ```

4. Update the `.env` file with your Supabase credentials:

   ```
   PORT=3000
   SUPABASE_URL=your_supabase_project_url
   SUPABASE_ANON_KEY=your_supabase_anon_key
   ```

5. Set up your Supabase database with the following schema:
   ```sql
   create table agents (
     id uuid default uuid_generate_v4() primary key,
     name text unique not null,
     personality text,
     created_at timestamp with time zone default timezone('utc'::text, now()) not null,
     updated_at timestamp with time zone default timezone('utc'::text, now()) not null
   );
   ```

## Development

Run the development server:

```bash
npm run dev
```

## Production

Build and start the production server:

```bash
npm run build
npm start
```

## API Endpoints

### Check if Agent Exists

```
GET /exists/:agentName
```

### Get Agent Data

```
GET /agent/:agentName
```

### Store Agent

```
POST /store-agent
Content-Type: application/json

{
  "agentName": "string",
  "agentDetails": {
    "personality": "string"
  }
}
```

## Error Handling

The API includes proper error handling and will return appropriate HTTP status codes:

- 200: Success
- 400: Bad Request
- 404: Not Found
- 500: Internal Server Error
