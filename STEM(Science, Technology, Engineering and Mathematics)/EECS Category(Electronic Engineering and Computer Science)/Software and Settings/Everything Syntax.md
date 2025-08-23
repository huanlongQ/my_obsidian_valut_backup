- [‎Gemini - Everything syntax](https://g.co/gemini/share/e1bfa2aa94f3) 
Of course. Here is a brief list summarizing the search syntax for the "Everything" software:

- **Basic Operators**
    
    - `space` = **AND** (e.g., `invoice report`)
        
    - `|` = **OR** (e.g., `invoice | report`)
        
    - `!` = **NOT** (e.g., `!draft`)
        
    - `"..."` = **Exact Phrase** (e.g., `"final project"`)
        
- **Wildcards**
    
    - `*` = Matches multiple characters (e.g., `doc*.pdf`)
        
    - `?` = Matches one character (e.g., `report_v?.docx`)
        
- **Common Functions (Modifiers)**
    
    - `path:<folder_path>` → Search within a specific folder.
        
    - `ext:<extension>` → Search for a file type (e.g., `ext:mp3;flac`).
        
    - `size:<value>` → Search by size (e.g., `size:>1gb`).
        
    - `dm:<date>` → Search by date modified (e.g., `dm:today`, `dm:lastweek`).
        
    - `dc:<date>` → Search by date created.
        
    - `dupe:` → Find duplicate files.
        
- **Combining Searches**
    
    - Chain functions together: `ext:mp4 size:>500mb !path:Backup`
        
    - Use parentheses `()` to group conditions: `(ext:pdf | ext:docx) dm:thismonth` 
