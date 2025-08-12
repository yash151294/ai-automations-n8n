# Instructions to use the ‘Framework for creating Automations through Claude Opus 4’  

1. Create a Project on Claude (I named it: N8N Workflow Builder)
2. Add the N8N documentation (in the GitHub folder) file to ‘Project Knowledge’ OR create your own N8N document (to update it) through the guide doc on how to pull N8N docs through GitHub
3. Add the System Prompt in the ‘Project Instructions’
4. In a thread inside the project, upload the ‘Claude Prompts Framework’ file and prompt it with:  
    <br/>Please help me craft a prompt based on the prompt framework, that I can share with my N8N workflow agent  
    <br/>Create an n8n workflow that \[primary objective\]. This workflow should be production-ready with proper error handling and documentation.  
    TRIGGER: &lt;Based on user preference&gt;  
    INPUT: &lt;Based on user input&gt;  
    PROCESSING: &lt;LLM of choice&gt;  
    OUTPUT: &lt;Where you want it&gt;  
    ERROR HANDLING: <>  
    The final output should be valid N8N JSON that can be imported into an n8n instance
5. Take the entire prompt generated and run it in a new thread in the same project after selecting ‘Claude Opus 4/4.1’ as your LLM
6. This will generate a JSON output as a response. Extract the JSON response and save it as a JSON file
7. Import the JSON in your n8n instance
